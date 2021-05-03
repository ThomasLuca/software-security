# Flow Analysis: Adding Sensitivity

To improve the flow analysis we'll add sensitivity.

## Sensitivity

### w/ Conditional

```C
int printf(untainted char *fmt, ...);
tainted char * fgets(...);
```

```C
char *name = fgets(..., network_fd);    // α
char *x = name;                         // β
if (...) x = name;
else x = "hello!";
printf(x)
```

Conditions:  
tainted <= α  
α <= β              // if true
untainted <= β      // if false
β <= untainted

if we leave out the third constraint, it is still illegal.

### Dropping the conditional

```C
int printf(untainted char *fmt, ...);
tainted char * fgets(...);
```

```C
char *name = fgets(..., network_fd);    // α
char *x = name;                         // β
x = name;
x = "hello!";
printf(x)
```

Conditions:  
tainted <= α  
α <= β  
untainted <= β  
β <= untainted

These constraints will result in a false alarm.

---

These examples were __flow sensitive__ each var has one qualifier which abstracts the taintedness of all values it ever contains.

### Reworked example

```C
int printf(untainted char *fmt, ...);
tainted char * fgets(...);
```

```C
\* α *\ char *name = fgets(..., network_fd);
\* β *\ schar *x1, \* Ɣ *\ *x2;
x1 = name;
x2 = "hello!";
printf(x)
```

Conditions:  
tainted <= α  
α <= β  
untainted <= Ɣ

There is no alarm, this is a good solution

### Multiple conditions

```C
int printf(untainted char *fmt, ...);
tainted char * fgets(...);
```

```C
void f(int x) {
    \* α *\ char *y
    if (x) y = "hello!";
    else y = fgets(..., network_fd);
    if (x) printf(y);
}
```

Conditions:  
untainted <= α  
tainted <= α  
α <= untainted

No solution, this lack of solution is a false alarm.
