---
title: "Assembly Refresher (Module 3)"
description: ""
date: 2021-09-03T20:11:00-07:00
lastmod: 2021-09-03T20:11:00-07:00
cover: ""
coverAlt: ""
toc: false
tags: ["pwn.college"]
draft: false
---
<style>
	main {
    margin: 90px auto;
    padding: 0 15px;
    max-width: 70%;
	}
</style>

*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili’s [pwn.college lectures](https://pwn.college/modules/asm) from the “Assembly Refresher” module. Much credit goes to Yan’s expertise! Please check out the pwn.college resources and challenges in the sources*

This module relies heavily on preexisting x86 knowledge, so if you don't have experience with x86 then I'd recommend starting with [Resources](#resources) and learning some of the basics or the rest of this post won't make much sense.

## Table of Contents
- [Registers](#registers)
- [Instructions](#instructions)
- [Memory](#memorystack)
- [Resources](#resources)

## Registers
Registers: very fast, temporary storage for data
- The address of the next instruction is stored in a register (eip)
- General purpose registers (eax, ecx, edx, ebx, esp, ebp, esi, edi)

**Partial Register Access:**

A full register is 64 bits long, however they can be accessed partially. The below table show the layout of the different registers, followed by an image explaining the layout of the rax register:

![amd64 Partial Access Sheet](../allPartialAccessOnAMD64.jpeg)
![Partial Register Access Visual](../partialRegisterAccess.png)
- *WARNING:* Accessing eax will zero out the rest of rax
    - all other partial access will preserve untouched parts of the register

## Instructions
- Tell the CPU what to do
- Take several different forms, generally include:
    - Opcode: what to do
    - Operands: what to do it on/with
- Flow right to left (take whats on the right and move it into the left register)
- Control flow is determined by conditional and unconditional jumps
    - Unconditional: call, jmp, ret
    - Conditional:
![Types of Conditionals](../conditionals.png)
![Conditional Bit Layout](../conditionalBitLayout.png)
- Conditionals key off the "flags" register (eflags)
    - eflags register is updated by:
        - arithmetic operations
        - cmp - subtraction (`cmp rax, rbx`)
        - test - and (`test rax, rax`)
- System calls will stop the process, request the OS to perform a task, and once the task is completed the OS will resume the process
    - Triggered by:
        - setting rax register to the system call number
        - storing arguments in rdi, rsi, etc.
        - calling the `syscall` instruction
    - Have very well-defined interfaces that very rarely change
    - A maintained list of all the system calls (over 300 in Linux) are [here](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)

## Memory(stack)
**Fulfils Four Main Issues:**
1. Track the "callstack" of a program.
<br><div style="padding-left: 2em;">[ ] return values are "pushed" to the stack during a call and "popped" during a ret</div>
2. Contain local variables of functions
3. Provide scratch space (to alleviate register exhaustion)
4. Pass function arguments
<br><div style="padding-left: 2em;">[ ] always on x86
<br>[ ] only for functions with "many" arguments on other architectures</div>

## Resources:
- [x86 Register Cheat Sheet](https://web.stanford.edu/class/cs107/resources/x86-64-reference.pdf)
- [x86 Assembly Guide](https://www.cs.virginia.edu/~evans/cs216/guides/x86.html)
- [Tutorial to Write a Program in x86](https://cs.lmu.edu/~ray/notes/nasmtutorial/)
- [Language X to x86 Converter](https://www.godbolt.org/)
- [Ryan A. Chapman Linux System Call Table](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)

## Sources
- [pwn.college Module 3 Lectures](https://pwn.college/modules/asm)
- [pwn.college Module 3 Challenges](https://dojo.pwn.college/challenges/asm)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)
