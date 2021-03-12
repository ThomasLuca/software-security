# Code Injection
There are two challenges for code injection:
    1. Load my own code into memory.
    2. Somehow get %eip to point at it.

## Load code into memory
* It must be the machine code instructions (i.e., already compiled and ready to run)
* It can not contain any all-zero bytes (eg: sprintf, gets, scanf,...) otherwise the code will stop copying. The code should also be complete (can't use the loader)

### What code to run?
* In the best case; a __general-purpose shell__
    * This is a command-line prompt that gives attacker access to the system.
* The code to launch a shell is called __shellcode__
Shell code might look like this:
```C
#include <studio.h>
int main(){
    char *name[2];
    name[0] = "/bin/sh";
    name[1] = NULL;
    execv(name[0], name, NULL);
}
```
This translates to the following assembly
```assembly
xorl %eax, %eax
pushl %eax
pushl $0x68732f2f
pushl $0x6e69622f
movl %esp, %ebx
pushl %eax
```
## Getting injected code to run
We don't know where our malicious code is stored with respect the the instruction pointer.
So the goal is to get the instruction pointer at the start and start running.
<br>
We can manipulate the instruction pointer to point at our code by overriding the address of %eip with the address of our code. Then when the function returns the instruction pointer will go the that exact address and start running the code.
<br>
<br>

__Now how do we know to which address we want the instruction pointer to go?__

There are a few different techniques:
* Trial and error. Keep trying until something works -> This possible won't work due to the large address range
* Use a __nop sled__ (a single-byte instruction which simply moves to the next instruction). Injecting a bunch of nop sleds in front of the malicious code will eventually bring the pointer to the code if the pointer happens to land on a nop sled.

```
________________________________________________________________________________
| text |...|    buffer  |%eip return address| nop nop nop ...| malicious code   |
________________________________________________________________________________
```