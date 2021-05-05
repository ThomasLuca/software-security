# Pen Testing

Pen testing is he process of trying to find exploitable vulnerabilities in complete systems or system components.

Once patterns of exploration and exploitation emerge, you write tools to do the work.

## Pen testing's bag of tricks

* Knowledge about the target domain (eg: the web)
* How is the system build
  * Protocols
  * Languages
  * Frameworks
* Common weaknesses
  * Bugs (eg: SQL injections, XSS, CSRF)
  * Misconfigurations, bad design (default passwords)

## Web hacking

* 70%: Messing with parameters (eg URL)
* 10%: Default passwords
* 10%: Hidden files and directories
* 10%: other
  * Insecure web services
  * Auth problems

## Tools

Used to:

* Probe a target
* Gather information
* Exploit a vulnerability

The tool depends on the goal and the target.

### Nmap

* Nmap = Network Mapper
  * what hosts on the network
  * what services these hosts offer
  * what OS the hosts are running
  * Packet filters/ firewalls in use
* Works by sending ip packets
  * ICMP echo request / Timestamp
  * TCP SYN to port 433,  TCP SYN/ACK to port 80
  * Probes to TCP ports
  * Probes to different responses on different OSes
* Be stealthy
  * Emit packets at other rates to avoid getting detected

### Web proxies

Web proxies sit between the browser and the server. Then display which packets are exchanged and can result in modification by an attacker.

#### Zap (Zed Attack Proxy)

* GUI-based inspection tool for capturing packets
* Can set breakpoints to allow packets through until a condition is met.
* Additional features
  * Active scanning: attempts XSS, SQL injection,...
  * Fuzzing: context-specific payloads
  * Spider: explores the site to construct model of system

Also see __Burp__

### Metasploit

* Advanced open-source platform for developing, testing and using exploit code
* Script attacks
  * Probe remote site and look for vulnerable services
  * Construct payload based on versions
  * Encode payload to avoid detection
  * Inject payload
  * Wait for shellcode to connect back (command prompt)

### 100's of modules & scripts

* Exploits against certain vulnerabilities
* Password sniffing
* Privilege escalation
* Keylogging & backdoors
* ...

### Kali

* Linux distro with a lot of pentesting tools pre installed
  * John the Ripper (password cracking)
  * Valgrind (dynamic binary analysis)
  * Reaver (Wifi password cracking)
  * peepdf (scanning pdf files for attack vectors)
