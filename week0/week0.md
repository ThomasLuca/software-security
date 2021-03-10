# Introduction
## Computer Security

* __What is computer security?__: security is about correctness. A system should do waterer it is desired to do without any _undesired behavior_

* __Kinds of undesired behaviors__:
    1. Confidentiality: stealing of information
    2. Integrate: modifying information or functionality (eg: destroying record / installing unwanted software)
    3. Availability: Dining access

* __Defects and vulnerabilities__: problem in software's design and implementation which causes it to behave incorrectly
    * __Flaw__: defect in design
    * __Bug__: defect in implementation

_To ensure security, we must eliminate bugs and design flaws, and/or make them harder to exploit._

## Software Security

* __What is software security?__: 
    * a kind of computer security that focuses on the __secure design and implementation of software__ (finding the best language, tools and methods).
    * It focusses on the __code__ (by contrast ignoring the code and focus on firewall & anti-virus, ...)

### Why software security?
Other securities do not suffice.

#### OS
the OS can make sure that a program doesn't get access to data/ports it shouldn't get access to.

##### Limitations
* OS cannot enforce __application specified__ policies (eg DB management system (DBMS))
* OS cannot enforce __into-flow__ policies

#### Firewall and IDSs
Firewall and IDS __observe__, __block__ and __filter messages__ exchanged by programs.
<br>
The firewall can only allow access to a server on port 80.
An IDS can examine packets and recognize part of a known exploit pattern and filter them out.

##### Limitations
Firewall will allow access to certain ports like port 80 because it thinks it is meant for normal web-traffic.
There are also techniques to access blocked ports by disguising the port with port 80. (SOAP)
<br>
IDSs can make networks slow by processing packets. This results in vulnerabilities like (D)DOS-attacks.

#### Anti-virus
Looks fore malicious behavior in local files.

##### Limitations
Easy to bypass with attack vectors.