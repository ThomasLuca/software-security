# Challenges and Variations

* Taint through operators
  * If an argument to an operator is tainted, then the expression containing that operator is too.
* Function pointers
  * Use flow analysis to compute possible targets (precise but not efficient)
* Struct fields
  * Analysis can track taintedness of the same field of all  instances of a struct (not that precise but very efficient)
* Array
  * Track taintedness of each element / track on the entire array
  * Problem: arrays are computed in stead of const so it's hard to track them at compile time.

## Other kinds of analysis

* Pointer analysis
  * Determines if two pointers are possibly aliases (can they point to the same memory?)
* Data flow analysis
  * Determines which vars are still alive (can their values still be read in the future)
* Abstract interpretation
  * Abstraction must discard information (eg: which calls respond to which returns). The key is to discard as much information as possible.
