# Static Analysis: Introduction part 2

## What can Static Analysis do?

### The Halting Problem

Can we write an analyzer that can prove, for
any program P and inputs to it, whether P will terminate?

The answer is "No". An analyzer will always fail to produce some answers for at  least some programs/inputs.

### Other properties?

* Prove that all array accesses are in bounds? (avoid buffer overruns)
  * The answer is undecidable (these properties can be converted into the halting problem)
* Other undecidable properties:
  * Does this SQL string come from a tainted source?
  * Is this pointer used after its memory is freed?

#### Halting ≃ Index in Bounds example

Proof by transformation

* Change index expression to exit

```C
(i >= 0 && i < a.length) ? a[i] : exit()
```

Now all array bounds errors instead result in terminators.

* Change program exit points to out-of-bounds accesses

```C
a[a.length+10]
```

If the bounds checker finds an error, the program halts. If it doesn't find an error, the program does not halt. This is in contradiction with the undecidability of the halting problem.

## Is Static Analysis impossible?

__Perfect__ static analysis is __impossible__. But it is still quite useful despite the following:

* Nontermination
* False alarms
* Missed errors

Nonterminating analyses are confusing to the user, that's why tools that exhibit false alarms and missed errors are the norm.

## The Art of Static Analysis

Analysis design tradeoffs:

* __Precision__: Model program behavior to minimize false alarms
* __Scalability__: Analyze large programs
* __Understandability__: Error reports should be easy to understand

=> Code style is important: An analysis with these 3 functions is easier to produce with clean code.
