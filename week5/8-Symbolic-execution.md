# Introducing Symbolic Execution

Software contains bugs. We can find them by testing & code reviews. But there are still al lot of missing bugs .Sometimes they are known but not important enough to fix. Other times, nobody knows about them.

Reasons:

* Bug is in a rare feature (driver)
* Bugs only occur in rare circumstances (on certain hardware)
* Bug could arise nondeterministic (circumstances that make bug arise are unpredictable)

## Static analysis

A way to find bugs that tests misses is with static analysis (consider all runs of a program).

But can static analysis find difficult bugs? _not often_ (It has to take into account: developer confusion, false positives, error management,...)

## Symbolic execution

A middle ground between testing and static analysis.

* Testing works (tons of bugs get reported and fixed because of it)
  * Problem: each test only explores one execution of a program (eg: `assert(f(3) == 5` is only tested for the input 3)
  * Tests are __complete__ but not __sound__.

* __Symbolic execution generalizes testing__
  * More __sound__ than testing. (eg: `y=a; assert(f(y)==2*y-1)`)
  * The symbolic program will execute until it depends on an unknown, then it will run tests for all possible values of that unknown.

  example:

  ```C
  int f(int x) {
      if(x > 0) {
          return 2*x-1;
      } else {
          return 10;
      }
  }
  ```

Another example:

```C
int a = α, b = β, c = Ɣ; //symbolic
int x = 0, y = 0, z = 0

if(a) {
    x = -2;
} if(b < 5) {
    if(!a && c) {
        y = 1;
    }
    z = 2;
}
assert(x+y+z != 3)
```

We can cover a lot more of a program's execution space than while testing.
