---
title: "Program Misuse (Module 2)"
date: 2021-09-02
tags: ["pwn.college"]
image : "/posts/programMisuse.png"
description: "Summary of pwn.college's Module 2 recorded lessons."
---
*Note: Most of the below information is summarized from Dr. Yan Shoshitaishvili's [pwn.college lectures](https://pwn.college/modules/misuse) from the “Program Misuse” module. Much credit goes to Yan's expertise! Please check out the pwn.college resources and challenges in the sources*

In module 2 there wasn't as much content to cover so this post isn't too long. I'd still recommend checking out the lectures yourself for demonstrations on each of the topics covered.

## Privilege Escalation
- Every process has a user ID (UID) and and a group ID (GID)
    - UID 0: the Linux admin user (root). Needed for:
        - Installing software
        - Loading device drivers
        - Shutting down/rebooting
        - Changing system-wide settings
        - Can be used to:
            - open ANY file
            - execute any program
            - assume any other user/group ID
            - debug any program

### **Linux Permission Model:**
![Linux Permission Model](../linuxPermissionModel.png)
- SUID(Set User ID): execute with the eUID(effective user ID) of the file owner rather than the parent process
    - Reset every time a file's ownership is changed
- SGID(Set Group ID): execute with the eGID(effective Group ID) of the file owner rather than the parent process
- Sticky: used for shared directories to limit file removal to file owners
    - ensures you can only delete files you have created in a shared directory
- Effective ID(eUID/eGID): the UID/GID used for most access checks
- Read ID(UID/GID):the "real" user/group ID of the process owner, used for things such as signal checks
- Saved ID: a user/group ID that your process could switch its eUID/eGID to
    - Used for temporarily dropping privileges

### Useful Commands:
- `id`: will list out the IDs of every process on your system
- `sudo chmod u+s fileName`: add the SUID for the given file
- `sh -p`: ensures that privileges are not dropped when running a program

## Sources:
- [pwn.college Module 2 Lectures](https://pwn.college/modules/misuse)
- [pwn.college Module 2 Challenges](https://dojo.pwn.college/challenges/misuse)
- [pwn.college Class Twitch Streams](https://www.twitch.tv/pwncollege)
