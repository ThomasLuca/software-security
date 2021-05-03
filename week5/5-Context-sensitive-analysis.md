# Context Sensitive Analysis

## Handling function calls

Function call example:

```C
α char *a = fgets(...);
β char *b = id(a);

δ char *id( char *x) {
    return x;
}
```

1. Give flow variable names to argument and return value (α, β)
2. Create flow constrains between caller and callee.

tainted <= α  
α <= Ɣ  
Ɣ <= δ  
δ <= β

Example with 2 extra statements:

```C
α char *a = fgets(...);
β char *b = id(a);
ω char *c = "hi";
print(c);

δ char *id(Ɣ char *x) {
    return x;
}
```

tainted <= α  
α <= Ɣ  
Ɣ <= δ  
δ <= β  
untainted <= ω  
ω <= untainted  

__No Alarms__: A good solution exists ω = untainted, α = β = Ɣ = δ = tainted.

But as small logical change to the program will cause a false alarm:

```C
α char *a = fgets(...);
β char *b = id(a);
ω char *c = id("hi");
print(c);

δ char *id(Ɣ char *x) {
    return x;
}
```

tainted <= α  
α <= Ɣ  
Ɣ <= δ  
δ <= β  
untainted <= Ɣ  
Ɣ <= ω  
ω <= untainted

tainted <= α <= Ɣ <= δ <= ω <= untainted

__False Alarm__: No solution, and yet no true tainted flow.

## Context (In)sensitivity

* Context sensitivity: solves this problem by _distinguishing call sites_ in some way.
  * We can do this by giving them a label and match them up with calls in the corresponding returns.

```C
α char *a = fgets(...);
β char *b = id➀(a);
ω char *c = id➁("hi");
print(c);

δ char *id(Ɣ char *x) {
    return x;
}
```

tainted <= α  
α <= -1 Ɣ  
Ɣ <= δ  
δ <= +1 β  
untainted <= -2 Ɣ  
Ɣ <=  +2 ω  
ω <= untainted

__No Alarm__: indexes don't match
