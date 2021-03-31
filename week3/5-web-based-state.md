# Web-based State Using Hidden Fields and Cookies

* The lifetime of an HTTP session is typically:
  * client connects
  * client requests
  * server responds
  * client requests something in the response
  * repeat
  * client disconnects

-> http has no notion of state of memory, http is stateless

## Maintaining State

* Web-app maintains _ephemeral_ state:
  * Server processing often produces intermediate results (no long-lived state)
  * Send such state to the client
  * Client returns the state in subsequent responses

There are two ways of implementing this:

* Hidden fields
* Cookies

### Capabilities

* Server maintains trusted state (while client maintains rest)
  * Server stores intermediate state
  * Send a _capability_ to access that state to the client

* Capabilities should be large, random numbers (hard to guess)

#### Hidden from fields

eg:

```html
<input type="hidden" name="sid" value="7893214">
```

```js
price = lookup(sid);
if(pay == yes && price != NULL){
    bill_creditcard(price);
    deliver_socks();
} else {
    display_transaction_cancelled_page();
}
```

Capabilities with hidden fields work, but they are impractical (we don't want to pass hidden fields around all the time).

### Statefulness with Cookies

* Server maintains trusted state
  * Server indexes state with a cookie
  * Send cookie to the client, which stores it
  * Client returns cookies with queries to the same server

#### Why use cookies

* Session identifier
  * After a user has authenticated
  * So the user doesn't have to authenticate each time
* Personalization
  * Let an anonymous user customize your site
  * Store fonts
* Tracker users
  * Advertisers want to know you behavior
  * Build a user profile across different websites (3rd party cookies)
