# Web 2.0

## Dynamic web pages

This is a web pages contain programs written in javascript. These programs will execute in the clients browser. To alter page content, js uses DOM objects. _Javascript can also read and modify cookies!_

## Danger

* Browsers need to confine javascript's power
* A script on attacker.com shouldn't be able tol
  * Alter the layout of bank.com
  * Read keystrokes typed by the user while on bank.com
  * Read cookies belonging to bank.com

## Defense

__Same Origin Policy (SOP)__:

* Browser provides isolation for js
* Browser associates web page elements (cookies, layout, ...) with it's origin.
