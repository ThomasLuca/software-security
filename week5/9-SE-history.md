# Symbolic Execution: A Little History

## The idea is old

First apposed in mid 1970's.

## Why didn't it take off?

* __It can be compute-intensive__
  * Lot's of possible paths
  * Need a query solver to decide on which paths are feasible
  * Program state has many bits

* At the time of invention, computers were __slow__ and __small__ (on memory).

## Rediscovery

* 2005-2006:
  * Heuristic search through space of possible executions
  * Find really interesting bugs
