# Static Analysis: Introduction part 1

A key element of a security conscious software development process is
performing code reviews with the assistance of tools. These tools use a technology called __static analysis__.

## Current Practice for Software Assurance

* __Testing__: make sure program runs correctly on set of inputs.
  * [+]: upon finding an error, it can be fixed.
  * [-]: expensive, difficult and hard to cover all code paths

* __Code Auditing__: Convincing someone else that your source code is correct.
  * [+]: Humans can generalize beyond single runs
  * [-]: Expensive, hard, no guarantees

* __Anayze program's code without running it__ (Static Analysis):  Ask a computer to do what a human could have done during code review.
  * [+]: higher coverage, reason about many runs of the program, reason about incomplete programs (libraries), provides a guarantee.
  * [-]: can only analyze limited properties, may miss some errors, can be time consuming to run

## Impact

* Encouraging better development practices (avoid mistakes and encourages a programmer to think about a mistake)
* Thoroughly checks limited but useful properties
