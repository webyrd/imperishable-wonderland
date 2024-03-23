% Confused Will’s Big List of Things He’d Like to Know about Relational Programming
% William E. Byrd
% March 22, 2024

Copyright 2024 by William E. Byrd

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). (CC BY 4.0) 

# What is this book?

This book describes questions related to relational programming and/or miniKanren that I am deeply curious about.  I provide a high-level description of each question, explain why I think the problem is interesting, give examples and code when I can, point to related resources, and discuss possible approaches to making progress.

# Why this book?

I want to clearly describe the problems I consider most interesting and most pressing in relational programming, in the hope that a clear problem description and examples may help me and my collaborators make progress.  Also, I hope these problems will inspire others, which will advance the state of relational programming further and faster than my colleagues and I could on our own.

# The writing philosophy behind this book

I want to record these problems quickly and simply, and provide enough details and resouces for someone familiar with miniKanren to easily get up to speed on the problems.

# Who is the audience for this book?

Anyone interested in understanding or pushing the state of the art in relational programming.  I assume that the reader is familiar with the basics of miniKanren and relational programming, and is unafraid of experimentation.

# Things I'd Like to Know about Relational Programming

## Can techniques like those used in Alpha Go and Alpha Zero, such as Monte Carlo simulation and reinforcement learning, provide radical speedups for program synthesis and other relational queries?

CPP'24 talk: claim of finding proof in 10^300 search space using Monte Carlo simulation + reinforcement learning

## How hard would it be to take relations expressed in Twelf/Coq/LambdaProlog, etc., and either extract miniKanren relations, or run the relations directly in those tools with more sophisticated search, etc.?

## Would implementing miniKanren constraints using constraint handling rules (CHR) make it easier to implement constraints?

## Is there a nice way to compose constraints in a way that is sound?  In particular, to allow multiple constraints to interact with each other for the same logic variable?  Would types remove this issue entirely?

## What would the equivalent of Chris Okasaki's 'Purely Functional Data Structures' book look like for relational programming?

## Can we create purely relational meta interpreters?

## Can we create purely relational abstract interpretation (perhaps involving tabling), and combine an abstract interpreter with a concrete interpreter in order to perform more interesting program synthesis?

## What are the best ways to encode implication and universal quantification in miniKanren?

## Can heterogenous towers of interpreters be collapsed?

## Would integrating a SAT or SMT solver into miniKanren allow for more efficient solving than when calling out to an external solver?

## Would implenting the Extended Andorra Model help us with conjunction in miniKanren?  (from Michael Ballantyne)

## Is there a relational, general version of `copy_term` from Prolog?

## What is the best way to implement relational aggregate operations?

## What are the tradeoffs inherent in encoding negation, aggregate operations, etc., via relational interpreter(s)?  At what level of nesting of interpreters (if any) does the "useful" expressive power "level off"?

## What is the semantic relationship between `append` in Scheme, `appendo` in miniKanren, and `append` in a relational Scheme interpreter in miniKanren?

## Is it possible to combine a relational parser, a relational type inferencer or type checker, and a relational interpreter into a single program that can perform program synthesis without entering "generate and test"?

## What exactly is going on in my experiment combining shallow and deep embeddings of miniKanren in miniKanren, where sharing fresh variables in the expression to be synthesized seems to combine the run* expressiveness with the efficienciency of a shallow embedding?  How far can this be pushed?  Is this behavior new, or has it been noticed before?  Does this behavior occur in other contexts?

## Is it possible to combine interpreters implementing operational semantics, axiomatic semantics, denotional semantics, etc., into a single program that can perform semantics-based synthesis and reasoning without entering "generate-and-test"?

## Is it possible to efficiently generate fixpoint combinators in a manner similar to how we can generate quines?

## Is it possible to make inherently small-step relations "fail fast"?

CESK

SKI