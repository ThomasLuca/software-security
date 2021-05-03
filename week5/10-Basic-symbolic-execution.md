# Basic Symbolic Execution

## Symbolic variables

Extends the language's support for expressions to include symbolic variables, representing _unknowns_.

## Symbolic expressions

* We make a language interpreter to be able to compute symbolically.
  * programs now contains symbolic expressions instead of only values.

| Normal values | Symbolic expressions          |
|---------------|-------------------------------|
|5, "hello"     |  α+5, "hello" + α, a[α+β+2]   |

## Straight line execution

```C
x = read();
y = 5 + x;
z = 7 + y;
a[z] = 1;
```

| Concrete memory | Symbolic memory |
|---|--|
|x -> 5|x -> α |
|y -> 10|y -> 5 + α |
|z -> 17|z -> 12 + α |
|a -> {0,0,0,0} Overrun!|a -> {0,0,0,0} Overrun!|

```C
x = read(); 
y = 5 + x;
z = 7 + y;
if(z < 0) {
    abort();
} if(z >= 4) {
    abort();
}
a[z] = 1;
```

If either lines 5 or 7 are reachable, we have found an out-of-bounds array access.

## Concolic execution (aka dynamic symbolic execution)

* Instrument the program to do symbolic execution on the side.
* Explore one path at a time, start to finish
* Concolic execution makes it easy to concretize
* It can do system calls
* Can handle conditions too complex for SMT solver
