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

## What are the connections between relational programming, reversible computing, program inversion, and bidirectional programming?

### Reversible computing and relational programming

#### Robert's 'Reversible computing from a programming language perspective' paper in TCS

* Reference [66] is to W. Kluge, 'A Reversible SE(M)CD machine', from 2000.  Would a reversible machine like this, or reversible or hybrid reversible-relational techniques, allow us to handle small-step reduction, etc., without "disconnecting the wires"?

* Implement RFUN, which is reference [118].  Also, look at Roshan and Amr's reversible language.  What happens if these languages are implemented in miniKanren?  What happens if miniKanren is implemented in these languages?  Is it possible to do synthesis, do computation with partially-ground terms, etc.?

* What would happen if you: 1) implemented a pure reversible language as a pure relation in miniKanren; 2) implemented pure miniKanren in a pure reversible language?  Which properties, if any, would be "inherited" by such embeddings?  What about relational-in-reversible-in-relational and reversible-in-relational-in-reversible, etc.?  Could you collapse such towers?  Stage the interpreters?

* The paper mentions hybrid reversible-irreversible langauges.  What would a hybrid reversible-relational language look like?  Which sorts of programs could you write in such a language?

* Implement a reversible pushdown automata -- something interesting must come out of this experiment!  What are the connections and differences between a reversible pushdown automata and a relational reversible pushdown automata?

* Has anyone implemented a full classical reversible gate or other reversible hardware, and actually measured the entropy/heat/etc.?  What about for quantum computing?  (I assume so for quantum, since Shor's algorithm has been implemented.)  What is the relationship between D-Wave and quantum adiabatic computers and reversible computing?

* What are good ways to think of procedure `uncalls` in reversible computing?  This seems like a very unusual idea.  Can we think of `call` and `uncall` in the Mercury sense, in which a relation has deterministic "forward" and "backward" modes, which are compiled into separate functions?  Or is there a conceptual difference?

* Is the restriction of not "overwriting" data automatically met in a pure functional program?  Or does ignoring an input value in a recursive call (for example) violate this property just as well as mutation?

* Can program inversion and reversible computing be used for synthesis in the miniKanren + relational interpreter manner?

* What are the connections between `uncall` in reversible computing and `uneval` in NBE?

* What exactly is `inverse interpretation` in reversible computing?

* Footnote 4 on page 2: `(N, D)` languages seem very under-represented.  Work exploring, including from a miniKanren/relational programming perspective.

* The references contain many interesting sounding papers that involve Turing machines, Lisp, autoata, garbage collection, ALUs, etc.  How many of these can be implemented in miniKanren?  How many can be implemented on FPGA?

## Can techniques like those used in Alpha Go and Alpha Zero, such as Monte Carlo simulation and reinforcement learning, provide radical speedups for program synthesis and other relational queries?

CPP'24 talk: claim of finding proof in 10^300 search space using Monte Carlo simulation + reinforcement learning [add link to video]

[add link to neural-guided search paper from Neurips 2018]

[add link to n-grams repo]

## How hard would it be to take relations expressed in Twelf/Coq/LambdaProlog, etc., and either extract miniKanren relations, or run the relations directly in those tools with more sophisticated search, etc.?

These tools seem to *almost* go the entire way to relational programming; you write programs as relations, and the tools are based on some form of logic.  However, these tools seem to miss the ability to run the resulting relations in a way that is useful for synthesis in the same way that the relational interpreter in miniKanren can be used for synthesis.

It is possible to extract an executable OCaml program from Coq.  Why not an executable relational program, perhaps in OCanren?

Nada Amin has shown that it is possible to port the quine-generating relational interpreter from miniKanren to Twelf.  And, apparently, the interpreter is nicer to write in Twelf, in at least some ways.  However, apparently Twelf doesn't support a complete, interleaving search.  Would it be possible to use the equivalent of a Prolog-style meta-interpreter in Twelf to change the default search?  Or just implement the search monad?

The CUP book describing LambdaProlog even gives a relational interpreter.  I was fully expecting to see the interpreter synthesizing programs.  Yet they only seem to run the program forward.  They seem mostly concerned with the mechanized meta-theory uses of LambdaProlog (HOAS, implication, etc.), just like in Twelf.  Fair enough.  But, since they are already going to the trouble of writing their programs as relations in an expressive logic programming language, why not also support the ability to run these relations using a complete, interleaving search, or some other search strategy that permits program synthesis?

## Would implementing miniKanren constraints using constraint handling rules (CHR) make it easier to implement constraints?

[TODO]

## Is there a nice way to compose constraints in a way that is sound?  In particular, to allow multiple constraints to interact with each other for the same logic variable?  Would types remove this issue entirely?

[TODO]

## What would the equivalent of Chris Okasaki's 'Purely Functional Data Structures' book look like for relational programming?

[TODO]

## Can we create purely relational meta interpreters?

[TODO]

## Can we create purely relational abstract interpretation (perhaps involving tabling), and combine an abstract interpreter with a concrete interpreter in order to perform more interesting program synthesis?

[TODO]

## What are the best ways to encode implication and universal quantification in miniKanren?

[TODO]

## Can heterogenous towers of interpreters be collapsed?

[TODO]

## Would integrating a SAT or SMT solver into miniKanren allow for more efficient solving than when calling out to an external solver?

[TODO]

## Would implenting the Extended Andorra Model help us with conjunction in miniKanren?  (from Michael Ballantyne)

[TODO]

## Is there a relational, general version of `copy_term` from Prolog?

[TODO]

## What is the best way to implement relational aggregate operations?

[TODO]

## What are the tradeoffs inherent in encoding negation, aggregate operations, etc., via relational interpreter(s)?  At what level of nesting of interpreters (if any) does the "useful" expressive power "level off"?

[TODO]

## What is the semantic relationship between `append` in Scheme, `appendo` in miniKanren, and `append` in a relational Scheme interpreter in miniKanren?

[TODO]

## Is it possible to combine a relational parser, a relational type inferencer or type checker, and a relational interpreter into a single program that can perform program synthesis without entering "generate and test"?

[TODO]

## What exactly is going on in my experiment combining shallow and deep embeddings of miniKanren in miniKanren, where sharing fresh variables in the expression to be synthesized seems to combine the run* expressiveness with the efficienciency of a shallow embedding?  How far can this be pushed?  Is this behavior new, or has it been noticed before?  Does this behavior occur in other contexts?

[TODO]

## Is it possible to combine interpreters implementing operational semantics, axiomatic semantics, denotional semantics, etc., into a single program that can perform semantics-based synthesis and reasoning without entering "generate-and-test"?

[TODO]

## Is it possible to efficiently generate fixpoint combinators in a manner similar to how we can generate quines?

[TODO]

## Barliman interpreter -- properties (associativity) and eigen variables for synthesis specification, instead of just concrete input/output examples (PBE)?

[TODO]

## Is it possible to make inherently small-step relations "fail fast"?

CESK

SKI