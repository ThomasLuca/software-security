# Design Category: Favor Simplicity

Keep the system so simple as it possible can be.

## Use fail-safe defaults

Some configuration or usage choices affect a system's security.

* Length of cryptographic keys (eg 2028-bit RSA)
* Choice of password (no default password)
* Which inputs are deemed valid (whitelist rather than blacklist)

## Do not expect expert users

Software designers should consider how the mindset of a user will affect security.

* Favor simple  user interfaces
  * natural/ obvious choice should be a secure choice
  * Don't let users make frequent security decisions
  * Help users see the effect of their security choices.

## Passwords

Problem: Easy to remember passwords are easy to guess.

Solution:

* Password manager
* Provide a password strength meter for the user.
* Force user to provide special characters.
* Combination: manager + meter
