# Symbolic Execution as Search, and the Rise of Solvers

## Search and SMT

Symbolic execution is simple and useful but __computationally expensive__.

Symbolic execution boils down to _a kind of search problem_. (search through a lot of possibilities to find bugs)

## Path explosion

* Usually can't run symbolic execution to exhaustion.
  * Exponential in branching structure
  * Loops on symbolic vars are even worse (a lot of potential paths)

## Symbolic execution vs Static analysis

* SE will eventually terminate while SA could be stuck forever.
* SE can unfortunately lead to false alarms.

## Basic search

* DFS (Depth-first): worklist = stack
* BFS (Breadth-first): worklist = queue

For symbolic search, BFS is the better option.

## Search strategies

* Prioritize search
  * to paths more likely to contain bugs
  * only run for a certain amount of time

### Randomness

We don't know which path to take so we can chose randomly.

Randomly restart search and take another path.

Drawback: reproducibility

### Coverage-guided heuristics

Try to visit statements we haven't seen before

* Keep a score of statements and amount it's used.
* Next statement should be the one with lowest score

### Generational search

Hybrid of BFS and coverage-guided search.

### Combined search

Run multiple searches at the same time. (alternate between them). Avoid one-size-fits-all solution