# Design Category: Trust With Reluctance

A system contains multiple parts. A secure system depends on the security of every part. Security can be improved by _reducing the needed trust_ in different parts.

There are multiple ways to do this:

* Using a better __design__
* Using a better __implementation process__
* By not making __unnecessary assumptions__ (don't assume 3th-party libraries are secure)

## Small Trusted Computing Base (TCB)

Keeping the TCB small reduces the susceptibility to compromise. A smaller TCB is easier to investigate, find and fix security flaws.

Example: __OS kernel__ a large kernel with multiple components (eg drivers) is less secure. A bug in a driver could be exploited which could give an attacker access to the kernel.

## Least privilege

Don't give a part of the system more privileges than it needs.

Example: __Text editors__ like vi and emacs have more privileges. If you use editors like this for applications like an email auth. This could also result in unwanted access to the kernel.

## Promote Privacy

A good system restricts flow of sensitive data as much as possible. Only components that have access to sensitive information can disclose it.

Example: Downloading a PDF with sensitive information has more chances of getting compromised than showing that PDF document in the browser.

## Compartmentalization

Isolate system components in a compartment or sandbox to reduces privileges.

Example: disconnecting a sensitive DB from the internet. Only make it accessible by direct terminals.

> SecComp: a computer security facility in the Linux kernel. seccomp allows a process to make a one-way transition into a "secure" state where it cannot make any system calls except exit(), sigreturn(), read() and write() to already-open file descriptors. [[wikipedia](https://en.wikipedia.org/wiki/Seccomp)]
