# Memory safety
A program is memory safe if:
* __Temporal safety:__ It only constructs valid pointer
    * created by mallocs
    * created by legal language operators
* __Spatial safety:__ It only uses a pointer to access memory that belongs to that pointer

## Spatial safety
* view pointers as triples (p,b,e)
    * __p__ is the pointer
    * __b__ is the base of the memory region it may access
    * __e__ is the bounds (extend) of that region
* Access allowed if `b<=p<=e-sizeof(typeof(p))`
* Operations should only change the value of p (prevents dereferencing a pointer)

example:
```c
int x;              // assume sizeof(int) = 4byte 
int *y = &x;        // p = &x, b = &x, e = &x+4
int *z = y+1        // p = &x+4, b = &x, e = &x+4
*y = 3;             // OK: &x <= &x <= (&x+4)-4
*z = 3;             // Bad: &x <= &x !<= (&x+4)-4
```

### No buffer overflows
example:
```C
void copy(char *src, char *dst, int len){
    int i;
    for (i=0; i<len; i++){
        *dst = *src;
        src++;
        dst++;
    }
}
```
A buffer overflow can only happen if len is greater than *src or *dst.

### No format string attacks
The call to `printf` dereferences illegal pointers.
```C
char *buf = "%d %d %d\n";
printf(buf);
```
The buf format string defines the expected extend of the stack. `Printf` is expected to be called with 3 int arguments but that is not the case in this example. Therefor `printf` will access data beyond its stack-frame and violate memory safety (buffer overflow).

## Temporal safety
A temporal safety violations occurs when trying to access undefine memory (undefined, unallocated or freed memory).
Freeing a pointer and then dereferencing is an example of temporal safety.

### No dangling pointers
Accessing a freed pointer violates safety:
```C
int *p = malloc(sizeof(int));
*p = 5;
free(p);
prinf("%d\n", *p)   // violation
```
The memory got dereferenced thus it no longer belongs to p.<br>


Accessing uninitialized pointer violates safety:
```C
int *p;
*p = 5;     // violation
```

### Integer overflows
Only allowed if they are not used to manufacture an illegal pointer:
```C
int f() {
    unsigned short x = 65535;   // short == 2 bytes -> largest == 65535
    x++;                    // overflows to become 0
    printf("%d\n"x);        // memory safe
    char *p = malloc(x);    // size-0 buffer!
    p[1] = 'a';             // violation
}
```
