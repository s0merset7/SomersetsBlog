---
title: "Memory Errors (Module 8)"
date: 2022-04-17
tags: ["pwn.college"]
image : "/posts/memoryErrors.png"
Description: "Summary of pwn.college's Module 8 recorded lessons."
---
*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili’s [pwn.college lectures](https://pwn.college/modules/memory) from the “Memory Errors” module. Much credit goes to Yan’s expertise! Please check out the pwn.college resources and challenges in the sources*

# Memory Errors (Module 8)

## Table of Contents
- [High-Level Problems](#high-level-problems-with-the-c-language)
- [Stack Smashing](#smashing-the-stack)
- [Causes of Corruption](#causes-of-corruption)
- [Stack Canaries](#stack-canaries)
- [Address Space Layout Resolution](#address-space-layout-resolution-aslr)
    - [Overwriting Page Offsets](#overwriting-page-offsets)
- [Causes of Disclosure](#causes-of-disclosure)
- [Sources](#sources)

## High-Level Problems (with the C language)
1. Trusting the Developer
    - C is very low level, and trusts the developer knows what they are doing, even if it doest make sense. C does not implicitly track things (i.e. a programmer can try and access an 11th value of a size 4 array)
2. Mixing Control Information and Data
    - Programs start with potentially user-influenced data already present in the stack that is spread throughout the stack and heap during execution. While user data is normally "non-control" data, it is stored *together* with "control" data
    - The stack has everything "jumbled together". Stored together and treated the same
        - local variables (of active and caller functions)
        - saved pointers to other places on stack/in memory
        - return addresses
    - **Memory Corruption** occurs when user-controlled data manages to spread into data that shouldn't be user controlled (via memory error)
        - When control data is overwritten (i.e., a return address), control flow can be redirected elsewhere (such as injected code)
3. Mixing Data and Metadata
    - Strings are null terminated in C based on the size of the character array. When null bytes are in the input or there are no null bytes at all, when compiled the string variable may no longer function as intended
4. Initialization and Cleanup
    - If memory is not cleaned up before/after it is used, C will not handle it
    - If memory is not properly deleted after use, the values may still exist and be accessed after deallocation
    - If memory is not properly initialized before use, then its value will be the memory that existed prior to allocation

## Smashing the Stack
- Common insecure C functions for user input are `gets`, `strcpy`, `scanf`, `sprintf` as they accept a pointer to user input and have no concept of the size of the value being pointed to, allowing for potential buffer overflows
- What can be corrupted in the presence of memory corruption vulnerabilities:
    1. Memory that doesn't influence anything (not very useful for code exploitation)
    2. Memory that is used in a **value** to influence mathematical operations, conditional jumps, etc.
    3. Memory that is used as a **read pointer** (or offset), allowing us to force the program to access arbitrary memory
    4. Memory that is used as a **write pointer** (or offset), allowing us to force the program to overwrite arbitrary memory
    5. Memory that is used as a **code pointer** (or offset), allowing use to redirect program execution
        - Most powerful is when a return address is overwritten to control what is executed next (i.e., jumping to arbitrary functions, arbitrary instructions, between instructions, or chain functionality)

## Causes of Corruption
1. Classic Buffer Overflow
    - Because C does not implicitly track buffer sizes, simple overwrites are common
        - Such as overwriting a return address with a different address
2. Signedness Mixups
    - Standard C library used *unsigned integers* for sizes while the default integer types (`short`, `int`, `long`) are *signed*
    - In x86, instructions such as `cmp` will return a flag based upon its result to inform the conditional instructions regardless of signedness. The conditional instructions however (such as `jae` and `jge`) may interpret results based on signed vs unsigned, yielding different decisions for the same `cmp` flag
3. Integer Overflows
    - Since C used two's compliment to store negative values, when calculations go from negative to positive numbers, allocated size may be negatively impacted
        - Example: If a space of `-1` is allocated, the code will handle that as `0xFFFFFFFF` which is the maximum integer allowed. However if that value is mathematically changed later to say `0`, then there is a larger amount of memory not being used that can be abused as a buffer overflow
4. Off-By-One Errors
    - If a developer makes the mistake of being "off-by-one" say in a comparative loop where memory is being accessed, this can allow for a small buffer overflow which may still break the program

## Stack Canaries
- Canaries are a buffer overflow mitigation technique based on real life canaries used in mines to detect poisonous gasses before it killed miners. The concept places a randomized value in the stack and will check if it has been "killed" (overwritten or altered) and if so, then terminated the program
- In general, stack canaries are VERY effective
- Ways in which to bypass canaries
    1. Leak the canary (using another vulnerability)
    2. Brute-force the canary (for forking processes)
    3. Jump the canary (if the situation allows)
        - depending on the stack layout, it may be possible to overwrite a value and redirect a read to point to *after* the canary

## Address Space Layout Resolution (ASLR)
- Memory corruption often focuses on corrupting *pointers* to point somewhere else. If the location of code and data in memory was randomized it makes corruption much more difficult
- Methods to redirect execution without knowing where code is
    1. Leak the Location
        - The addresses still (mostly) have to be in memory so that the program can find its own assets
        - Requires a different vulnerability
    2. YOLO
        - Program assets are *page aligned* meaning only part of the address is randomized (the page offset)
        - Brute force the page offset
    3. Brute-Force (situational)
        - For forking processes, the addresses can be brute forced

### Overwriting Page Offsets
- Pages are always aligned to a 0x1000 alignment
    - Possible page addresses are:
        - `0x00007f8dce27f000` (a library)
        - `0x56531c9c5000` (a main binary)
        - `0xffffffffff600000` (kernel mapped helper)
        - `0x400000` (non-position independent binary)
- The last 3 *nibbles* of an address are never changed
- If the two least significant bytes of a pointer are overwritten, there is only one nibble (4 bits) to redirect the pointer to another location on the same page
    - With little endian, these are the first two bytes that we will overwrite

## Causes of Disclosure
- Most memory corruption mitigation techniques (canaries and ASLR) rely on keeping a "secret" value(s) from an attacker
- Types of memory errors that lead to disclosure of these "secrets"
    1. Buffer Overread
        - analogous to buffer overflow but with reading instead of writing
    2. Termination Problems
        - In C, strings do not have explicit size metadata in memory
            - To solve this, they are *null-terminated*
        - If the null byte is forgotten, print functions that don't account for size will print until a null byte is found
            - Input can overflown to remove null bytes and print information from other parts in the stack
        - This does not work for canaries as in little-endian, they begin with a null byte, causing print statements to stop before printing their content
    3. Uninitialized Data
        - C will not clean up memory, and when memory is deallocated, it is not removed just dereferenced
        - Be cautious as some optimized compilers will remove attempts to clear memory as it is "costly" and seemingly "pointless"
            - Better to initialize variables to zero before using them

## Sources
- [pwn.college Module 8 Lectures](https://pwn.college/modules/reversing)
- [pwn.college Module 8 Challenges](https://dojo.pwn.college/challenges/memory)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)