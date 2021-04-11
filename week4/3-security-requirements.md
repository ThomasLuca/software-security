# Security Requirements

* Security-related goals or policies (eg: a user's bank account should not be read/modified by other users)
* Required mechanisms for enforcing them (eg: users identify themselves using a strong password)

## Typical Kinds of Requirements

* Policies
  * Confidentiality
  * Integrity
  * Availability

* Support mechanisms (Gold standards)
  * Authentication
  * Authorization
  * Auditability

---

### Confidentiality and Privacy

Sensitive information should not be leaked to unauthorized parties.

* Direct leak: via the software system's intended interaction mechanism
* Side channel leak: from measurements of other system features, like timing, power usage, or space usage

### Integrity

Sensitive information should not be damaged by unauthorized parties (eg: only the account owner can authorize withdrawals from her account)

* Direct: Being able to specifically withdraw from the account
* Indirect: tricking the system into withdrawing from someones account (eg: CSRF)

### Availability

A system is responsive to requests (a user should always be able to access their account)

* DoS attacks attempt to compromise availability.

---

### Authentication

What is the subject of security policies?  
Need to define a notion to identify and a way to connect an action with an identity.

### Authorization

Defines when a principal may preform an action.
(eg Bob can access his own account, but not the account of others)

### Audit

Retain enough information to be able to determine the circumstances of a breach or misbehavior. (that info is often stored in log files)
