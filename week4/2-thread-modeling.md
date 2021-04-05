# Thread Modeling, or Architectural Risk Analysis

To secure software, you should now what you are defending it against. Therefor, you should make a threat model which assumes the adversary's power.  
This is part of the architectural risk analysis.

## Example thread models

### Network User

An anonymous user that can connect to a service via network. A malicious net user could

* __measure__ the size and timing of requests and responses.
* run __parallel sessions__
* provide __malformed inputs/messages__
* __drop or send extra messages__

Example attacks: SQL injections, XSS, CSRF, buffer overrun/ ROP payloads,...

### Snooping User

Internet user on the __same network__ as other users of some service.  
Thus can:

* __Read__ other's messages
* __Intercept, duplicate & modify__ messages

Example attacks: Session hijacking, privacy-violating side-channel attack, DOS  
  
!! Don't assume that traffic is safe just because it's encrypted. Encryption can be undone by gaining info about packet size & timing in metadata

### Co-located User

Internet user on the __same machine__ as other users of some service.  
Thus can:

* __Read/write__ user's __memory and files__ (cookies, ..)
* __Snoop keypresses__
* Read/write the user's __display__

## Thread-driven Design

* __Network-ony attacker__ implies that message traffic is safe (no need for encryption)
* __Snooping attacker__ means message traffic is visible.
* __Co-located attacker__ can access local files and memory.

## Finding a good model

* Compare against similar systems
* Understand past attacks and attack patterns
* Challenge assumptions in design (risk assessment, take into account the potential costs of building a system, taking into account the potential cost of successful breaches & weighing the likelihood of each).
