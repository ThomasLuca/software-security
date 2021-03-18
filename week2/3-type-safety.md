# Type safety
* Insures that operation on the object are always compatible with the object's type.
* Type safety is stringer then memory safety:
```C
int (*cmp)(char*,char*);
int *p = (int*)malloc(sizeof(int));
*p = 1;
cmp = (int (*)(char*,char*))p;
cmp("hello","bye"); // crash
```
This example is memory safe but not type safe.<br><br>

Type safety __also__ applies to __dynamically typed languages__ (eg: python, javascript, ruby,...). These languages only have 1 type that all objects have. If data is not right for that object, the language will trow an exception.

## Enforce invariants
* Types are used to enforce invariants with invariants like function calls and array indexing.
* Enforcement of __Abstract types__ which can keep modules hidden from clients (isolation from rest of the program).

## Types for Security
Some languages have special typed system developed for enforcing security properties.
eg JIF (java with information flow):
```java
int{Alica->Bob} x;
int{Alice->Bob, Chunk} y;
x = y;      // OK: policy on x is stronger
y = x;      // BAD: policy on y is not as strong as x
```

## Why are languages without type safety still commonly used?
* Type safe languages tend to have worse performance (due to garbage collection, bounds checks & abstract representations).

## New high performance languages with type safety
* Go (Google)
* Rust (Mozzila)
* Swift (Apple)