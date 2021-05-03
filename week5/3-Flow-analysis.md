# Flow Analysis

Flow analysis tracks how values might flow between the different memory locations in a program.

This can help us find bugs with root cause of trusting unvalidated user input.
If tainted data (input from user) is used where untainted data is expected, there could be a serious vulnerability.
(eg: SQL injections or source string of `strcpy` whose length is greater then target buffer size)

## Goal

The goal is to make sure that tainted data can not reach an untainted sink. The aim is to develop a _sound_ analysis.

example:
Untainted data can reach tainted sink

```C
void f(tainted int);
untainted int a = ...;
f(a)        // This is valid
```

Tainted data should not reach an untainted sink:

```C
void g(untainted int);
tainted int b = ...;
g(b)        // This is invalid
```

### Steps

1. Create a name for each missing qualifier (e.g; α, β)
2. For each statement in the program, generate constraints on possible solutions (eg: q1 <= q2)
3. Sovle  the constraints to produce solutions for α, β
4. If no solution exists, there may be an illegal flow.

Example:

```C
int printf(untainted char *fmt, ...);
tainted char * fgets(...);
```

```C
char *name = fgets(..., network_fd);    // α
char *x = name                          // β
printf(x);
```

constraints:

* tainted <= α
* α <= β
* β <= untainted

This is an __illegal flow__: α can only be equal to a tainted value, and β only equal to untainted. As a result we get the following constraint tainted <= untainted which is illegal.
