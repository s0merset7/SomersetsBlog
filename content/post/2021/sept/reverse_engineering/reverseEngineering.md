---
title: "Reverse Engineering (Module 6)"
date: 2021-09-19
tags: ["pwn.college"]
image : "/posts/reverseEngineering.png"
Description: "Summary of pwn.college's Module 6 recorded lessons."
---
*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili’s [pwn.college lectures](https://pwn.college/modules/reversing) from the “Binary Reverse Engineering” module. Much credit goes to Yan’s expertise! Please check out the pwn.college resources and challenges in the sources*

## Functions and Frames

Control Flow Graphs: a way of visually representing a function
- graph: word used to describe the entire function map
- block: set on instructions that will execute one after the other
- edges: represent conditional/unconditional jumps
    - Blue (Unconditional Jump): a jump that will always be taken
    - Green (Conditional Jump): the condition is met (true)
    - Red (Conditional Jump): the condition is not met (false)
- prologue: sets up the stack frame
    - save off the caller's base pointer
    - set current stack pointer as the base pointer
    - "allocate" space on the stack (subtract from the stack pointer)
- epilogue: tears down the stack frame
    - "deallocate" the stack `mov rsp, rbp`
        - Note: data is NOT destroyed by default
    - restore the old base pointer
- stack frame: reserved place in memory for the stack to operate
    - stack pointer (rsp): points to the leftmost side of the stack frame
    - base pointer (rbp): points to the rightmost side of the stack frame

What is the stack:
- a memory region used to store local variables
    - when you `push` to the stack, `rsp` is *decreased* by 8
    - when you `pop` from the stack, `rsp` is *increased* by 8
- the stack starts out storing the environment variables and the program arguments (among other things)

## Data Access

Locations for Data:
- .data: used for pre-initialized global writable data (such as global arrays with initial values)
- .rodata: used for global read-only data (such as string constants)
- .bss: used for uninitialized global writable data (such as global arrays without initial values)
- stack: used for statically-allocated local variables
- heap: used for dynamically-allocated (malloc()ed) variables

## Static Tools

Static Tools: tools used to reverse engineer a program at rest

Simple Tools:
- [**kaitai struct**](https://ide.kaitai.io/): file format parser and explorer
- **nm**: lists symbols used/provided by ELF files
- **strings**: dumps ASCII (and other format) strings found in a file
- **objdump**: simple disassembler
- [**checksec**](https://github.com/slimm609/checksec.sh): analyzes security features used by an executable

Advanced Tools (Disassemblers):
- Commercial:
    - [**IDA Pro**](https://www.hex-rays.com/products/ida/): the "gold standard" of disassemblers
    - [**Binary Ninja**](https://binary.ninja/): IDA's main commercial competitor
- Free:
    - [**Binary Ninja Cloud**](https://cloud.binary.ninja/): a version of Binary Ninja that runs in your browser! 
- Open source:
    - [**angr management**](https://github.com/angr/angr-management/releases): an academic binary analysis framework!
    - [**ghidra**](https://ghidra-sre.org/): a reversing tool created by the National Security Agency
    - [**cutter**](https://cutter.re/): a reversing tool created by the radare2 open source project

## Dynamic Tools

Dynamic Tools: tools used to reverse engineer a program at runtime

Tools:
- **ltrace**: traces library calls
- **strace**: traces system calls
- **gdb**: used to walk through a program as it is running
    - gdb has its own scripting language, here's an example of it:
```
disp/5i $rip
break *0x401025
commands
    x/s $rsp
    c
end
```
- this will display the first five instructions of the code, then break right after the instruction located at *0x401025 is executed, and finally will display what is stored in the rsp register


## Sources
- [pwn.college Module 6 Lectures](https://pwn.college/modules/reversing)
- [pwn.college Module 6 Challenges](https://dojo.pwn.college/challenges/reversing)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)