# Defense against Low-Level Attacks: Introduction
## What did the low-level attacks have in common
1. Attacker was able to __control some data__ used by the program
2. Use of data permits __unintentional access to some memory area__ in the program

## Outline
* Vulnerabilities are caused by _memory safety_ and _type safety_
* Automatic defenses (changes how program is compiled or ran by hardware)
    * Stack canaries
    * ASLR (Address space layout randomization)
* __ROP__ attack (Return-oriented programming), a technique that can bypass previously mentioned defenses.
* __Secure coding__