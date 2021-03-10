# Buffer overflow attacks
* __Buffer__:  contiguous memory associated with a variable or field. (In C, strings are buffers (arrays of char's)).
* __Overflow__: Put more into the buffer than it can hold.

_Where does the overflowing data go?_ 

## Example of buffer overflow
```C
void func(char *arg1){
    char buffer[4];
    strcpy(buffer, arg1);
    ...
}
int main(){
    char *mystr = "AuthMe!"
    func(mystr);
    ...
}
```
You can already see that copying a string of 8 characters into a buffer of 4 characters is going to cause some problems. Here's what happens
```
______________________________________________________
|      A u t h |   %ebp    |   %eip    |   &arg1    | |
______________________________________________________
        buffer |   M e ! \0|
```
This results in a segmentation fault
<br>
Following example shows how buffer overflows can be used to perform an attack

```C
void func(char *arg1){
    int authenticated = 0;
    char buffer[4];
    strcpy(buffer, arg1);
    if(authenticated) {...
}
int main(){
    char *mystr = "AuthMe!";
    func(mystr);
    ...
}
```
```
   buffer     authenticated    
_____________________________________________________________________
|   A u t h | 4d 65 20 00    |   %ebp    |   %eip    |   &arg1    | |
_____________________________________________________________________
            |   M e ! \0     |
```
This time the buffer will override the authenticated variable, which will not result in an error.
This means that the when the authenticated variable is called, some other code will be executed.
Attackers can abuse this by intentionally overflowing a buffer whit executable malicious code.