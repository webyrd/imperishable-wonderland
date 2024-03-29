% How I Think About Relational Programming
% William E. Byrd
% March 27, 2024

Copyright 2024 by William E. Byrd

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). (CC BY 4.0) 

# What is this book?

An attempt to describe some of my mental models for thinking about relational programming, especially in the context of miniKanren and its variants.

# Why this book?

The topic of how an experienced relational programmer/miniKanren programmer and researcher thinks about the relational paradigm seems to me to be worthy of its own short book, especially since discussion of the mental models I have developed over time, or that I have learned from others, feels different in character than a book or paper on the techniques of relational programming, or the features of miniKanren, or what-have-you.

# The writing philosophy behind this book

I'd like to keep the book short, and focused on mental models.

# Who is the audience for this book?

Anyone interested in a higher-level conceptual understanding of miniKanren and relational programming.

# Introduction --- How I think about relational programming

[TODO]

# Table metaphor for mk/relational programming.

A common way to represent data is as a *table*.  For example, we can represent addition of two integers `x` and `y`, each of which is an integer between 0 and 3 inclusive, and whose sum is the integer `z`, as the table:

+---+---+---+
| x | y | z |
+===+===+===+
| 0 | 0 | 0 |
+---+---+---+
| 0 | 1 | 1 |
+---+---+---+
| 0 | 2 | 2 |
+---+---+---+
| 0 | 3 | 3 |
+---+---+---+
| 1 | 0 | 1 |
+---+---+---+
| 1 | 1 | 2 |
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
| 1 | 3 | 4 |
+---+---+---+
| 2 | 0 | 2 |
+---+---+---+
| 2 | 1 | 3 |
+---+---+---+
| 2 | 2 | 4 |
+---+---+---+
| 2 | 3 | 5 |
+---+---+---+
| 3 | 0 | 3 |
+---+---+---+
| 3 | 1 | 4 |
+---+---+---+
| 3 | 2 | 5 |
+---+---+---+
| 3 | 3 | 6 |
+---+---+---+

[TODO figure out how tables work in the Pandoc Markdown extension]

[lookup table --- can perform addition by finding the table entry with the desired values of `x` and `y`.]

[can perform subtraction in the same manner!  don't need to construct a new table --- just need to use the existing table slightly differently]

[more generally, can use the table to find solutions to the equation/relation `x + y = z`]
[like algebra --- solve for `x`, etc.]
[for a given `z`, can solve for unknown `x` and `y`, which will have multiple solutions]

[the table need not be finite!  Can allow `x`, `y`, and `z` to be natural numbers, for example]
We can represent addition of two natural numbers (non-negative integers) `x` and `y`, whose sum is the natural number `z`, as the table:

+---+---+---+
| x | y | z |
+===+===+===+
| 0 | 0 | 0 |
+---+---+---+
| 0 | 1 | 1 |
+---+---+---+
| 0 | 2 | 2 |
+---+---+---+
| 0 | 3 | 3 |
+---+---+---+
|...        |
+---+---+---+
| 1 | 0 | 1 |
+---+---+---+
| 1 | 1 | 2 |
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
| 1 | 3 | 4 |
+---+---+---+
|...        |
+---+---+---+
| 2 | 0 | 2 |
+---+---+---+
| 2 | 1 | 3 |
+---+---+---+
| 2 | 2 | 4 |
+---+---+---+
| 2 | 3 | 5 |
+---+---+---+
|...        |
+---+---+---+
| 3 | 0 | 3 |
+---+---+---+
| 3 | 1 | 4 |
+---+---+---+
| 3 | 2 | 5 |
+---+---+---+
| 3 | 3 | 6 |
+---+---+---+
|...        |
+---+---+---+

[infinite table --- can't write it down completely, since we'd never finish; we need to be *lazy*, and avoid generating the entire table before producing a result]

[not only can have multiple solutions, but can have *infinitely many* solutions; we need to avoid asking for all the solutions when there are infinitely many, unless we can also be lazy in handling the potentially infinite *stream* of solutions]

[DFS won't find all solutions]

[need for complete search]


# Logic programming vs. constraint programming vs. constraint logic programming vs. functional programming vs. functional logic programming vs. relational programming.

# How to think about what a `run` means, how to interpret the answers produced, etc.

[TODO]

# A modern view of unification in logic programming.

[TODO]

# Is relational programming better done in Prolog?

[TODO]

# Types and relational programming?

[TODO]

# How to think about `==` and `=/=`.

[TODO]

# Confusion people have with `=/=`.

[TODO]

# How to think about `absento`.

[TODO]

# Confusion people have about `absento`.

# Why program relationally?

[TODO]

# Purity --- friend or foe?

[TODO]

# Constraints and consistency/inconsistency + many worlds interpretation---OS process metaphor.

[TODO]

# Dan Friedman -- search strategy as an OS scheduling independent processes; complete search means that processes that don't diverge will run to completion, given enough time and memory.

[TODO]

# properties/desiderata of `run`, mk goals, etc.

[program slicing in that online Prolog book]

# When to design and implement a new constraint

[TODO]

# Performance

[TODO]

# Data representation

[TODO]

# Laziness

[TODO]

# Motivation for mk constraints.

[TODO]

# Connection with SQL, etc.

[`Simply Logical` -- very nice and readable book on logic programming with the SQL analogies in the last few chapter]
