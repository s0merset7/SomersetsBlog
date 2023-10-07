---
title: "Shellcoding (Module 4)"
date: 2021-09-06
tags: ["pwn.college"]
image : "/posts/shellcodingPost.png"
Description: "Summary of pwn.college's Module 4 recorded lessons."
---
*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili’s [pwn.college lectures](https://pwn.college/modules/shellcode) from the “Shellcode Injection” module. Much credit goes to Yan’s expertise! Please check out the pwn.college resources and challenges in the sources*

This module relies heavily on preexisting x86 knowledge, so if you don't have experience with x86 then I'd recommend taking a look at the [last post](https://s0merset7.github.io/posts/assembly_refresher/assemblyrefresher/) and learning some of the basics or the rest of this post won't make much sense. I would HIGHLY recommend also watching the lecture videos as you are able to see actual examples of what is explained here.

## What is Shellcode
- Most computer architectures treat code and data interchangeably, allowing us to manipulate data as code
    - We can use shellcode to abuse this
- The "traditional" goal with shellcode is to launch a shell (`execve("/bin/sh", NULL, NULL)`)
    - want to achieve arbitrary command execution
    - not always to launch a shell (read a file we don't have permissions for)
- We can add data into out shellcode
    - use `.byte` or `.string`

To write shellcode, need this format:
```
.global _start
_start:
.intel_syntax noprefix
    your shellcode
```
- This will set up a global symbol to indicate the start of the shellcode (`.global _start`)
    - This allows us to execute our code as a normal ELF file
- Indicate where the start is (`_start:`)
- Indicate that we are using Intel x86 instead of AT&T x86

Then we need to assemble it:
 - `gcc -nostdlib -static shellcode.s -o shellcode-elf`
    - `nostdlib`: indicate we don't want to use the standard libraries since we are instead calling them directly using systemcalls in the code
    - `-static`: indicate we are only loading our code and are not dependant upon anything else
    - `-o shellcode-elf`: output the compiled code into a file called "shellcode-elf"

The previous command will only create a program, not shellcode. To get the shellcode we need to do:
- `objcopy --dump-section .text=shellcode-raw shellcode-elf`
    - In our ELF file, there is a `.text` section that contains our shellcode. By running this command, we are *dumping* the `.text` *section* of the code into a new file we call "shellcode-elf"

**Debuging:**
- After compiling your code with the instructions above, you can debug your code by running `strace ./shellcode-elf`
    - This will display everything being executed by your code, which will often assist in finding any unwanted activity
- **gdb** is a Linux command that allows you to walk through your code as it runs `gdb ./shellcode-elf`
    - Caveats:
        - there is no source code to display and navigate.
        - to print the next 5 instructions: `x/5i $rip`
        - you can examine qwords (`x/gx $rsp`), dwords (`x/2dx $rsp`), halfwords (`x/4hx $rsp`), and bytes (`x/8b $rsp`)
        - to step one instruction (follow call instructions): `si`, NOT `s`
        - to step one instruction (step over call instructions): `ni`, NOT `n`
        - to break at an address/label: `break *0x400000` or `break labelName`
        - `run`, `continue`, and [reverse execution](https://sourceware.org/gdb/onlinedocs/gdb/Reverse-Execution.html) work as expected
    - You can hardcode breakpoints
        - breakpoints are implemented with the `int3` instruction
        - you can place this anywhere yourself!
        - especially useful at the start of shellcode to catch the beginning of shellcode execution

## Common Challenges
- Sometimes shellcode will not be allowed to use certain bytes as a result of how the program processes it like:
![Problematic Methods](../problematicMethods.png)
- We can get around some of these restrictions by being creative:
![Creative Workarounds](../creativeWorkarounds.png)
- Remember that data and code are interchangeable from the computers point of view, so we can data to our code as bytes that is called by other commands
    - when doing this, make sure to have `.text` writeable by running `gcc -Wl, -N --static -nostdlib shellcode.s -o shellcode-elf`

## Sources
- [pwn.college Module 4 Lectures](https://pwn.college/modules/shellcode)
- [pwn.college Module 4 Challenges](https://dojo.pwn.college/challenges/shellcode)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)
- [Ryan A. Chapman Linux System Call Table](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)
