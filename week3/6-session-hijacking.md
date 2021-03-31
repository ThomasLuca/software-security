# Session Hijacking

## Cookies and web authentication

* Cookies are commonly used for authentication
* If user logs in with correct credentials, the server will associate them with a session cookie
* Another request to the server will always send that session cookie to avoid having to log-in again.

## Cookie Theft

* Session cookies are capabilities (holder of this cookie has the privileges of the user that got the cookie for login-in)
* Stealing a cookie can result in impersonation.

## Stealing Session Cookies

* __Compromised__ browser/server
* __Predict__ the cookie bases on other information you know
* __Sniff__ the network
  * __DNS cache poisoning__: tricking the user into thinking you are the right server

## Defence: Unpredictability

* Avoid theft by guessing: cookies should be
  * Random
  * Long
* Server can also require separate, correlating information (same IP / browser)
* Time out session IDs and delete them once session ends.
