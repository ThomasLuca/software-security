# Cross-Site Request Forgery - CSRF

* Get requests should be reads of the server state but unfortunately they can also modify the state

example:  

* Client is logged in to the bank
* Client is searching the internet and comes across a malicious site (attacker.com)
* attacker.com returns a page which contains a reference to the url of the bank (`<img src="http://bank.com/transfer.cgi?amt=9999&to=atacker">`)
* Browser automatically visits url to obtain what it believes to be an image.
* Client will thus send a request to bank.com
* Since user is already logged in to bank.com, the request will be accompanied by the session id that includes the cookie that says that the user was authenticated.
* Bank.com will perform the request

---

* __Target__: user who has account on vulnerable server
* __Attack goal__: make request to server via users browser
* __Attacker tools__: get the user to click on a link that goes to vulnerable site.
* __Key tricks__: Requests to the web server have predictable structures. Use something like an html image tag to send the request.

## CSRF protection

### Referer

* The browser will set the __REFERRER__ field to the page that hosted a clicked link.
* Server could check that the request has a referrer fields that only contains trusted urls.
  * Problem: referrer fields is optional
  * Response: use Lenient referrer check
    * Blocks requests with bad referrer, but allows requests with no referrer
  * Problem: no referrer can still be harmful.
    * Attacker can force remove the referrer
      * Bounce user off of ftp: page
      * Exploit browser vulnerability
      * Man-in-the-middle network attack

### Secretized Links

Include a secret in every link/form

* Can use a hidden form field, custom HTTP header, or encode it directly in the URL
* Must not be guessable value
* Can be same as session id sent in cookie.

Frameworks can help in doing this (Ruby on Rails automatically embeds secrets in every link).

eg: <http://website.com/doStuff.html?sid=81ad5554daeer8e>
