# Avoiding Flaws with Principles

* Flaws = Defects in the design
* Bugs = Defects in the implementation

Around half of security problems are caused by flaws.

## Design vs Implementation

* Highest level: about man actors (eg programming language, browser, DB management system,...)
* Next level: decomposition of actor into modules/components.
* Next level: how to implement data types and functions.

## Secure Software Design

Design software architecture according to good principles and rules.

## Principles and Rules

* Principle: high-level design goal with many possible manifestations
* Rule: a specific practice that is consonant with sound design principles.

The software design phase tends to focus on principles to avoid flaws.

## Categories of Principles

* Prevention
  * Goal: Eliminate software defects entirely.
  * Example: Heartbleed bug wouldn't have happened if they used a type-safe language

* Mitigation
  * Goal: reduce the harm from exploitation of unknown defects
  * Example: Run each browser tab in a separate process (exploitation of one tab doesn't effect other tabs)

* Detection and Recovery
  * Goal: Identify and understand attack
  * Example: Monitoring and snapshotting

## Principles

* Favor simplicity (use fail-safe defaults)
* Trust with reluctance (grant the least privilege possible)
* Defend in depth (no security by obscurity)
* Monitor and trace
