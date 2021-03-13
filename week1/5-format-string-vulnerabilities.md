# Format string vulnerabilities
Example of C's printf supported formatted I/O
```C
void print_record(int age, int char *name){
    printf("Name: %s\tAge: %d\n, name, age");
} // %s = string    %d = integer
```
Bad implementation of this formats can lead to vulnerabilities.
```C
printf("%s", buf);  // Safe implementation
printf(buf);        // Vulnerability
```
If buf contains format specifiers, those will just be printed out in the first example. In the second example, the format specifiers will be interpreted. This can lead to an attack.

## Formats in memory
```C
int i = 10;
prinf("%d %p\n", i, &i);           
```
```
________________________________________________________________________
|       ...        |  %ebp  | %eip | &fmt | 10 | &i |      ....         |
                   <------printf's stack frame-----><-caller's stack frame->
```
```C
void vulnerable(){
    char buff[80];
    if(fgets(buf, sizeof(buff), stdin) == NULL)
        return;
    printf(buf);
}       
```
```
________________________________________________________________________
|       ...                |  %ebp  | %eip | &fmt |       ....         |
                   <-----printf's stack frame----><-caller's stack frame->
```
If printf interprets a string with formats, it will try to read formatted data from the caller's stack frame.