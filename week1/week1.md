# Low Level Security
## Intro
What will we learn this week:
    * Buffer overflow attacks
    * History of buffer overflow attacks
Buffer overflow = any access of a buffer outside of its allotted bounds

## Memory Layout
All programs are stored in memory. A program that starts running is called a __process__. 
This process is given memory by the OS in order to run.
```
_____________________ 0xffffffff
|   cmdline & env   | > Set when process starts
|                   |
|   Stack           | \
|                   |  \ Runtime
|   HEAP            |  /
|                   | / 
|   Uninit data     | \
|                   |  \
|   Init data       |     Known at compile time
|                   |  /
|   Text            | /
_____________________ 0x00000000
```
* __Stack__: holds local variables and metadata that program uses to go and return from functions
* __Heap__: Area that malloc manages
* __Uninit__: eg static int x;
* __Init__: eg static const int y = 10;

## Memory allocation
Heap grows to higher address & stack grows to lower address. They grow towards each other.
<br>
<br>
A program contains a __stack pointer__ (%esp) which points at border of stack. When push function is issued, the stack pointer will move after pushing the value. If a function returns, the stack pointer will move back to it's initial place removing all the recently created variables.
<br>
<br>
The heap is mostly apportioned by the OS managed by malloc. 

## Basic stack layout.

```C
void func(char *arg1, int arg2, int arg3){
    char loc1[4]
    int loc2;
    ...
}
```
```
<----------------------Stack Frame----------------------->
____________________________________________________________________________
... | loc2 | loc1 |      ????       | arg1 | arg2 | arg3 |  callers-data |  |
____________________________________________________________________________ 
    ^             ^                 <--------------------
    | %esp        | %ebp
```
Now if the function wants to increment loc2, the stack pointer doesn't know the absolute address at compile time. Thats why a __Stack frame__ contains a __Frame pointer__ (%ebp) so now it can maintain a relative path.

<br>

__Calling a function__

    1. Push arguments onto the stack
    2. Push the return address (the address of the instruction you want to run after control returns to you)
    3. Jump to the function's address

__Called function__

    4. Push the old frame pointer onto the stack (%ebp)
    5. Set the frame pointer to where the end of the stack is right now
    6. Push the local variables onto the stack (right of the epb pointer)

__Return function__

    7. Reset the previous stack frame: %esp = %ebp, %ebp = (%ebp)
    8. Jump back to the return address: %eip = 4(%esp)
(%eip = instruction pointer)
