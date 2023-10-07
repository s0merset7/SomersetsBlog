---
title: "Dynamic Allocator Misuse (Module B)"
date: 2022-04-23
tags: ["pwn.college"]
image : "/posts/dynamicAllocatorMisuse.png"
Description: "Summary of pwn.college's Module B recorded lessons."
---
*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili’s [pwn.college lectures](https://pwn.college/modules/heap) from the “Memory Errors” module. Much credit goes to Yan’s expertise! Please check out the pwn.college resources and challenges in the sources*

# Dynamic Allocator Misuse (Module B)

## Table of Contents
- [The Heap](#the-heap)
    - [Types of Memory](#types-of-memory)
    - [How the Heap Works](#how-the-heap-works)
        - [The Data Segment](#the-data-segment)
- [Dangers of the Heap](#dangers-of-the-heap)
- [Thread Local Caching (tcache)](#thread-local-caching-tcache)
    - [Freeing](#what-happens-on-free)
    - [Allocating](#what-happens-on-allocation)
- [Metadata and Chunks](#metadata-and-chunks)
- [Sources](#sources)

## The Heap

### Types of Memory
- **ELF .text**: Where the code lives
- **ELF .plt**: Where the library function stubs live
- **ELF .got**: Where pointers to imported symbols live
- **ELF .bss**: Used for uninitialized global writable data
    - Example: global arrays without initial values
- **ELF .data**: Use for pre-initialized global writable data
    - Example: global arrays with initial values
- **ELF .rodata**: Yse for global read-only data
    - Example: string constants
- **Stack**: Local variables, temporary storage, call stack metadata
- **Heap**: Place to store long-lived *dynamic* memory
    - Example: variable-length list

### How the Heap Works
- The heap works by initially allocating a large chunk of memory space, but only supplying smaller parts of that space to a program as needed
- It is implemented by ptmalloc/glibc (and analogues) and uses the following main functions (not an exhaustive list):
    - `malloc()`: allocate some memory
    - `free()`: free a prior allocated chunk
    - `realloc()`: change the size of an allocation
    - `calloc()`: allocate and zero-out memory

#### The Data Segment
- Historical oddity from segmented memory spaces
- With ASLR, placed randomly into memory near the PIE base
- Starts with a size of 0
- managed by the `brk` and `sbrk` system calls
    - `sbrk(NULL)`: returns the end of the data segment
    - `sbrek(delta)`: expands the end of the data segment by `delta` bytes
    - `brk(addr)`: expands the end of the data segment to `addr`
- This process is managed just like `mmap()`
- ptmalloc slices off bits of the data segment for small allocations, and uses `mmap()` for large allocations

## Dangers of the Heap
Why is the heap vulnerable:
1. Used by imperfect human programmers
    - forget to free memory
        - leads to resource exhaustion
    - forget all the spots where pointers to data are stored
    - forget what's been freed
        - using free memory
        - freeing free memory
    - corrupting metadata used by the allocator to keep track of heap state
        - conceptually similar to corruption internal function state on the stack
2. A library that strived for performance
    - allocation and deallocation needs to be fast, or programs will slow down
    - optimizations often leave security as an afterthought

### Double Freeing
- Pointers to an allocation remain valid after `free()`ing the allocation, and are sometimes `free()`d again
- New versions of glibc/ptmallloc introduced the `key` check
    - If `key` is overwritten, then the heap can be abused

## Thread Local Caching (tcache)
- tcache in ptmalloc is used to speed up repeated (small) allocations in a single thread
    - A caching layer with very few security checks
- Implemented as a **singly-linked** list, with each thread having a list header for different-sized allocations

### What Happens on `free()`
1. **Select** the right "bin" based on the size
2. **Check** to make sure the entry hasn't already been freed (double-free)
3. **Push** the freed allocation to the front of the list
4. **Record** the tcache_perthread_struct associated with the freed allocation (for checking against double-frees)

### What Happens on Allocation
1. **Select** the bin number based on the requested size
2. **Check** the appropriate cache for available entries
3. **Reuse** the allocation in the front of the list if available

Things NOT done:
- clearing all sensitive pointers (only `key` is cleared)
- checking if the `next (return[0])` address makes sense

## Metadata and Chunks
- ptmalloc uses lots of metadata to track its operation and is kept in:
    - Global metadata (the tcache structure)
    - Per-chunk metadata
        - A "chunk" is what `malloc()` is actually tracking, and the address seen by programmers is just the usable memory AFTER the headers in the chunk

## Sources
- [pwn.college Module B Lectures](https://pwn.college/modules/heap)
- [pwn.college Module B Challenges](https://dojo.pwn.college/challenges/heap)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)