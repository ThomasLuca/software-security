# Symbolic Execution System

## SAGE

* SE system developed by Microsoft based on DART
* Uses generational search
* Target is to find bugs in file parsers (JPEG, DOCX, ...)
* Found over 3.4 billion constraints

## KLEE

* Symbolically executes LLVM bitcode (compiler used by Apple)
* Random path + coverage-guided
* Targets file access, system calls, ...

## Mayhem

* Runs on binaries
* Uses symbolic and concolic strategies
* Automatically generates exploits when bug is found

## Mergepoint

* Extends Mayhem with veritesting technique
* Symbolic execution + static analysis
* Analyses complete code blocks
* Better balance between solver and executor
  * __Faster to find bugs__
  * __Covers more of the program__ in the same time
* Found more than 12000 bugs in the linux kernel.
