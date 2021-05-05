# Fuzzing

A kind of random testing ( testing in which inputs for a test case are generated randomly or semi randomly.)

The goal is to make sure that crashes, hangs don't happen.

Fuzzing is very useful but limiting.

## Black box fuzzing

* Tool knows nothing about program
* Easy to use
* Explores only shallow states unless it gets lucky

## Grammar based fuzzing

* Tool generates input informed by a grammar.
* More work to use
* Can go deeper in the state space

## White box fuzzing

* Tool generates new input partially informed by the code of the program being fuzzed
* Easy to use
* Computationally expensive

---

There are different ways to generate inputs.

## By mutation

Takes legal input and mutates it. (inputs can be automated or human produced)

## Generional

Generates input from scratch (eg: from grammar)

## Combination

Generate initial input, mutate it, generate new input, mutate it, ...
They can also be mutations according to grammar

---

There are different ways fuzzers are used

## File-based fuzzing

* Mutate or generate inputs
* Run the target program with them
* See what happens

## Network-based fuzzing

* Act as one half of a communicating pair
  * Sends messages to a target program, trying to crash it
  * Inputs can ones again be made via grammar or mutations
* Act as man ini the middle
  * Mutating inputs exchanged between parties

---

## Dealing with crashes

* What is the cause?
  * Are crashes signaling the same bug?
* Does the crash signal an exploitable vulnerability?
  * Buffer overruns

## Finding memory errors

The problem is that the program will not immediately crash, only when the manipulated memory is reused.

* Make program crash on initial buffer override
  1. Use an __Address Sanitizer__ (ASAN)
  2. Fuzz it
  3. If program crashes with ASAN-signaled error, then worry about exportability
