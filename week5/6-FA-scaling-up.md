# Flow Analysis: Scaling it up to a Complete Language and Problem Set

So far we've considered scalar values or pointers treated as blocks.
But we haven't considered dereferences through pointers and
how those affect the tainting.

## Pointers

```C
α char *a = 'hi';
(β char *) *p = &a;
(Ɣ char *) *q = p;
ω char *b = fgets(...);
*q = b
printf(*p)
```

untainted <= α  
α <= β
β <= Ɣ
tainted <= ω
ω <= Ɣ
β <= untainted

__Solution exists:__ α = β = untainted & ω = Ɣ = tainted. This is a _problem that analysis will fail to uncover_ (tainted <= ω <= Ɣ <= β <= untainted).

## Flow and pointers

An assignment via a pointer flows both ways. This presents the opportunity to cause false alarms.
Reducing the alarms is possible by:

* Not assigning pointers to a `const` (then backwards flow is not needed)
* Drop backward flow edge (this isn't a good solution because it can cause other errors)

## Implicit flow

```C
void copy(tainted char *src, untainted char *dst, int len) {
    untainted int i;
    for (i = 0; i<len; i++){
        dst[i] = src[i]; // illegal
    }
}
```

```C
void copy(tainted char *src, untainted char *dst, int len) {
    untainted int i, j;
    for (i = 0; i<len; i++){
        for(j = 0; j<sizeof(char)*256; j++){
            if (src[i] == (char)j)
                dst[i] = (char)j; // legal
        }
    }
}
```

Although this inefficient example is legal, it also misses a flow. The same characters as the source was assigned to the new variable.

## Information flow analysis

We can perform information flow analysis to discover when such implicit flows happens (Data did not flow, but the information did)

eg:

```C
tainted int src;
α int dst;
if(!src){
    dst = 0;
} else {
    dst = 1;
}
dst += 0;
```

x = y  
label(y) <= label(x)  
pc <= label(x)

This solution works, but it's not commonly used. The code is bad for performance, can also lead to false alarms (ignore values).
