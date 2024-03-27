% Will's Big Bad Boring Braindump on Relational Programming
% William E. Byrd
% March 22, 2024

Copyright 2024 by William E. Byrd

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). (CC BY 4.0) 

# What is this book?

This book is intended to be a semi-structured brain dump of what I know about relational programming, constraint logic programming, miniKanren and its variants, and related topics.

# Why this book?

I started the book on Friday, March 22, 2024.  I have started working on another book, 'An Imperishable Wonderland of Infinite Fun', which is intended to be a highly-curated and highly-polished collection of interesting, unusual, and weird relational programs that I hope will inspire people to explore relational programming.  I have also been talking recently with students and researchers and hobbyists who are interested in learning about miniKanren and relational programming, from the implementation, application, theory, and fun perspectives.  Since I'm curating miniKanren resouces for 'An Imperishable Wonderland of Infinite Fun', and talking regularly with people interested in miniKanren, this seems like the perfect time to make a Big Bad Boring Braindump book.

# The writing philosophy behind this book

Get it done!

"Write badly, with pride" -- Eric Edson, [Film Courage interview](https://www.youtube.com/watch?v=V6Yql0jrjow at 19:00)

I remembered this as "Write poorly, proudly!", which I prefer slightly.)

Get all the ideas in my head down on paper as quickly as possible.  "The worst finished book is better than the best unfinished book" [something like that --- find exact quote in the Film Courage video I linked to in a recent video; add reference]

Dean Wesley Smith's notion of working at "pulp speed" also inspires me to write a book "into the dark" [something like that --- find exact phrase in DWS book; add reference]  Just sit down and start typing!

# Who is the audience for this book?

People who are trying to learn about miniKanren and/or relational programming and/or constraint logic programming, etc., at a deeper level than can be found in 'The Reasoned Schemer' or the original microKanren paper.  If nothing else, I hope you will find your own connections and inspiration in this semi-random collection of relational programming lore.  You are almost guaranteed to stumble across some ideas or techniques or artifacts or perspectives that you haven't seen before, even if you have been programming for a very long time.

# What is relational programming?

Relational programming is a programming paradigm in which computations are modeled as mathematical (or logical) relations.  This is in constrast, for example, to functional programming, in which computations are modeled as mathematical functions, mapping inputs to outputs.  Unlike most approached to programming, relational programming dispenses with the notions of inputs and outputs.  Instead, a relations takes zero or more *terms*, and each term can contain zero or more *logic variables* (also known as *unification variables*) that can represent unknown values.  Relational programs *constrain* these terms (including the logic variables in these terms) using *constraints*, such as *syntactic equality* and *syntactic disequality*.  A constraint logic reasoning engine performs a (potentially very sophisticated) mixture of constraint solving and search in an attempt to find assignments to the logic variables that satisfy all the constraints.  If the relational program includes recursion, there may be multiple solutions to one of these constraint problems, including infinitely many solutions.  Alternatively, the constraint logic engine might search an infinite search space looking for a non-existent solution to a constraint problem; in this case, the constraint logic engine may end up *diverging* (looping foreer), or may able to prove in finite time that no solution exist (*finite failure*).

# What is miniKanren?

miniKanren is a family of constraint logic programming languages, each of which is implemented by one or more constraint logic reasoning engines.  Many implementation of miniKanren focus on logical purity, emphasizing the relational aspects of computation.  Some variants of miniKanren-like languages, such as core.logic in Clojure, focus more on pragmatic uses of the language, as part of the program logic in a "standard" application.  Other variants, such as OCanren in OCaml, explore the relational aspects from a research perspective.

Most miniKanrens are implemented as *embedded domain-specific languages* (EDSLs), meaning that they extend some *host language* with additional functions, methods, etc., supporting the miniKanren language, along with an implementation in the host language of a constraint logic reasoning engine.  Historically miniKanren has been implemented in variants of Lisp (for example, Scheme, Racket, and Clojure) or other functional languages (OCaml and Haskell).  There has also been some work on implementing miniKanren as a stand-along language and run-time.

# What is microKanren?

microKanren (also written "muKanren" or "muKanren" [change to Greek 'mu' character]) is a minimal version of miniKanren created by Jason Hemann and Daniel P. Friedman [cite paper and github repo].  The original microKanren paper includes a tutorial reconstruction, including a step-by-step reconstruction of how to arrive at the interleaving search strategy, given how simpler search strategies can't find answers that exist in infinite search spaces.

microKanren is designed to be easily ported to other languages. The canonical core microKanren implementation is fewer than 50 lines of Scheme, and does use Scheme macros.  It is possible to implement miniKanren on top of microKanren, which is especially convenient in languages that supportsyntactic extension through macros (such as most Lisps, Rust, etc.).  A standard exercise for anyone learning miniKanren is to implement a version of microKanren in a host language of their choice.  As a result, microKanren has been implemented hundeds or thousands of times in dozens of host languages.  The main [miniKanren website](http://www.minikanren.org) contains links to many microKanren implementations---the website used to keep track of every microKanren implementation, but the number of implementations quickly became overwhelming.

# What is Kanren?  What are the similarities and differences between Kanren and miniKanren?

Kanren is the language that came before, and inspired, miniKanren.  Like miniKanren, the canonical Kanren implementation is an embedded domain-specific language in Scheme, using a combination of functions and Scheme hygienic macros.  Like miniKanren, Kanren is based on first-order syntactic unification and a complete, interleaving search strategy.  Kanren programs are written at a "higher level" that miniKanren programs.  The notion of extending relations is a concept built into Kanren.  Unlike miniKanren, Kanren performs unification over the terms passed into a Kanren relation.  Kanren's implementation includes an optimization inspired by Prolog called `head-let`, which is metaphorically equivalent to `project`ing the terms that are passed into a relation.  Kanren uses pattern matching, and has syntax that is similar in spirit to the clauses in Prolog (at least if you squint).

miniKanren can be thought of as a "lower level" language than Kanren---for example, there is no notion of extending relations, or of pattern matching, built into miniKanren; since miniKanren is not based on pattern matching, there is no `head-let` optimization built into miniKanren.  miniKanren could be thought of as a simpler, lower-level language that a Kanren program might compile (or macro-expand) to, in the same way that a miniKanren program might compile (or macro-expand) to microKanren.

# What does the name 'Kanren' mean?  Where did the name come from?

'Kanren' is the Japanese word for 'relation' [include kanji].  Oleg Kiselyov came up with the name.

# Where is the code for the miniKanren implementation from 'The Reasoned Schemer'?  How do they differ?

## Code from the second edition of 'The Reasoned Schemer' (2018)

The code from the second edition of 'The Reasoned Schemer' can be found [here on GitHub](https://github.com/TheReasonedSchemer2ndEd/CodeFromTheReasonedSchemer2ndEd)

## Code from the first edition of 'The Reasoned Schemer' (2005)

The code from the first edition of 'The Reasoned Schemer' can be found [here on GitHub](https://github.com/miniKanren/TheReasonedSchemer)

## The main differences between these implementations of miniKanren:

* The miniKanren language in the first edition contains two versions of conjunction, disjunction, and unification: `conde` and `condi`; `fresh` and `freshi`; `==` and `==-check`.  The second edition simplifies the language, and uses only the "safe" (interleaving/occurs-check) versions: the `==` from the second edition is equivalent to `==-check`, the `code` from the second edition is equivalent to `condi`, and `fresh` from the second edition is equivalent to `freshi`.

* The miniKanren implementation in the second edition is built on a modified version of microKanren.  As a result, there is a simple "core" language of binary disjunction and conjunction at the heart of the 2018 implementation.  Also, the syntactic forms (`run`, `fresh`, `conde`), which are implemented using Scheme hygienic macros, are cleanly separated from the underlying functions, to allow the implementation to be more easily understood by readers unfamiliar with Scheme hygienic macros, and to make it easier to port the non-macro parts of miniKarnen to other host languages that do not have macros or other syntactic abstraction mechanisms.

# Where is the original code for Kanren, and early work on miniKanren?

The original Kanren project, including documentation and code, can be found [here on SourceForce](https://kanren.sourceforge.net/)

# Are there any interesting ideas from the original Kanren language, implementation, and examples?

Yes, most definitely.  Kanren is underexplored at this point.

[relational extension]

[pattern matching syntax and `head-let`]

[separation of facts from rules]

[extended type inferencer and fixpoint trick]

[mirror of mirror]

[other theorem proving and equational reasoning goodness]

Exercise: build a Kanren on top of miniKanren, complete with the Kanren syntax, `head-let`, etc.

Exercise: replicate all the example applications in miniKanren, and extend/improve upon these examples

Exercise: use the ideas from these example applications to explore other theorem-proving and equational-reasoning programs in Kanren/miniKanren

# What are the tradeoffs of implementing miniKanren/microKanren as an embedded domain specific language?

Advantages of implementing miniKanren as an embedded domain specific language include:

* the implementation can use parts of the host language's implementation---for example, the existance of pairs, symbols, and numbers in Scheme;

* programmers can get the benefits of a (constraint) logic programming language, without having to give up the features and libraries and runtime of the host language---for example, Clojure programs can write a sophisticated application in Clojure, making full use of the JVM and the many Clojure and Java libraries, while adding logic programming functionality through `core.logic` (David Nolen's miniKanren-inspired EDSL in Clojure);

* miniKanren or microKanren can be quickly or easily ported to almost any host language, on various runtimes/platforms;

* the small size of miniKanren, and especially microKanren, makes it quick and easy to modify or extend the implementaion.

Disadvantages of implementing miniKanren as an embedded domain specific language include:

* there is not a single "canonical" implementation or set of libraries that the entire miniKanren community uses;

* the miniKanren community is itself somewhat fragmented, based on host language;

* the ease of implementation has resulted in hundreds or thousands of simple implementations of microKanren, and a fair number of implementations of miniKanren, which can seem overwhelming to anyone new to miniKanren;

* the embedded domain specific language approach can make whole-program optimization, compilation, and other techniques challenging or impossible.

# What are the differences between miniKanren and other logic or constraint logic programming languages?

[TODO]

# The Prolog elephant in the room

## How does miniKanren differ from Prolog?

[TODO]

## Can't you do all of this in Prolog?

[TODO]

## Shouldn't you just be using Prolog?

[TODO]

## Isn't miniKanren just warmed-up Prolog?

[TODO]

## But Prolog is useful...

[TODO]

## Etc.

[TODO]

# What are the supposed advantages of relational programming?

[TODO]

# What are the supposed disadvantages of relational programming?

[TODO]

# What are the major research themes in relational programming?

[TODO]

# What is a "relational interpreter"?

[TODO]

# What are the major implementations of miniKanren-inspired languages?

[TODO]

# What are experimental implementations of miniKanren-inspired languages under development?

## OCanren

[TODO]

## probKanren

[TODO]

## alphaKanren

[TODO]

# What are the main learning resources for miniKanren and relational programming?

[TODO]

# What are the main resources for someone wanting to learn about miniKanren and/or relational programming from a research perspective?

[TODO]

# What came before miniKanren?

[TODO]

# How has miniKanren changed over time?

[TODO]

# What is the difference between logic programming, constraint programming, constraint logic programming, and relational programming?

[TODO]

# Truth versus success/failure

[gets into why negation can be tricky]

# Many-worlds interpretation of logic programming

[includes the OS processes view]

# Prolog

## Standard resources for learning Prolog

'The Art of Prolog' -- esp. on meta-interpreters

'Clause and Effect'

'ISO Prolog'

'The Craft of Prolog'

'Learn Prolog Now'

[Ivan Bratko book on AI programming]

[the book that includes defeasible logic programming -- link to the free version on author's website]

[online book that discusses program slices]

## Cool things about Prolog

### Prolog syntax

* meta programming

* syntactic extensions (disjunction) and restrictions (Datalog, ASP) naturally map onto extensions/restrictions to the logics expressed, and the computational power/expense/guarantees of those logics

### Prolog meta interpreters

[clauses are in the global database]

[call]

### Many implementations, some with very interesting extensions

* Ciao Prolog

* Andorra Prolog

* CLP(X) extensions (for example, in SWI-Prolog)

* Constraint Handling Rules extensions [which Prologs support this?]

## Less cool things about Prolog (from the perspective of relational programming)

### Prolog, purity, and the default language choices

DFS as default choice

no occur-check as default choice

purity, or lack of it:

* `!` (cut) --- and its different "colors"

* `copy_term`

* `set_of`, `bag_of`, etc.

Many Prolog programmers seem to think that if their program doesn't
contain "red" cuts, their program is "declarative".  Whether the
program is declarative may be debatable.  However, most likely it
isn't *relational*.

## Translating Prolog programs to miniKanren

[TODO]

# Restrictions to logic programming

[Datalog]

[ASP]

# Extensions to logic programming

[higher-order unification and pattern matching]

[lambdaProlog]

[nominal logic programming]

# Modes

[TODO]

# Closed world vs. open world

## CWA

[TODO]

## OWA

[TODO]

## train table example

[TODO]

## Semantic Web, description logic, etc.

[TODO]

# Negation and negative information

## Negation as failure

[TODO]

## Constraints and regstricted negation

[TODO]

# Aggregation

[TODO]

# setof, bagof, etc.

relational implications of

# Stratified queries

[TODO]

# Nested `run`

[TODO]

# Stratified negation

[TODO]

# Relational programing techniques

## Relational arithmetic

[explore tradeoffs, laziness, domains, floundering, supported operations, etc.]

### passing a ground number as an argument and using normal arith operations

[TODO]

### `project` and normal arithmetic operations --- allows for logic variables and unification, so long as the arithmetic operations aren't used on a fresh logic variable

[TODO]

### delayed goals --- often can have some relational behavior, in that different "modes" can be supported: + and -, sin and arcsin, etc.

[TODO]

### Peano, and how it is good for increment and decrement

[TODO]

### "Oleg arithmetic" [include FLOPS paper, Prolog version, mk version, talk about proofs, decidability, performance, lazy vs. non-lazy, partally-instantiated numerals and which numbers they can represent, etc.]

[TODO]

### CLP(FD)  cKanren, core.lgic, etc.

[TODO]

### CLP(Z)

[TODO]

### CLP(R)

[TODO]

### bit vector constraints  [does this make sense?]

[TODO]

### CLP(SMT)   different solvers and the theories they support, smt-lib, solvers with sin and cos, etc.

[TODO]

# Various types of logic

## Monotonic vs. non-monotonic reasoning

[TODO]

## Nominal logic

[TODO]

## Defeasible logic

[TODO]

## Linear logic

[TODO]

## Probabilistic logic

[TODO]

## Temporal logic

[TODO]

## Modal logic

[TODO]

# Functional logic programming

[TODO]

# Logic and constraint logic programming languages

## miniKanren

[TODO]

## Prolog

[TODO]

## Datalog

[TODO]

## Answer Set Programming

[TODO]

## Problog

[TODO]

## PRISM

[TODO]

## Mercury

[TODO]

## Verse/Verse Calculus -- similarity to Icon

[TODO]

## Curry -- laziness and needed narrowing

[TODO]

## Godel [dots over the o] [include the successor language]

[TODO]

## [include other languages, esp. older ones]

[TODO]

# Constraint solving

## Modern view of traditional logic programming as CLP(Tree); Prolog 0 with disunification

[TODO]

### disequality constraints --- H. Comon paper; Prolog 0 and Prolog II; not sure why the Prolog that caught on didn't seem to include disequality constraints

[TODO]

## Modern Prologs support various constraint domains

[TODO]

## CLP(X), typed or sorted logic variables, and combining constraints from various domains on a single variable

[TODO]

# Search

## DFS

[TODO]

## BFS

[TODO]

## IDFS

[TODO]

## Interleaving search

[TODO]

## Guided search

### A* search

[TODO]

### Neural-guided search

[TODO]

### N-grams guided search

[TODO]

### Probabilistic search: sequential MC, etc.

[TODO]

# Unification

## Variants of unification

### First-order syntactic unification

[TODO]

### Nominal unification and equivariant unification

[TODO]

### Higher-order unification and higher-order pattern matching

[TODO]

### Unification with segment variables [should this be thought of as a type of e-unification?]

[TODO]

### E-unification

#### ACI unification

[representing subtyping etc. in unification and logic programming]

# Relational parsing

[TODO]

# Relational type checking and inference

[TODO]

# The heachaches and how to deal with them:

## Conjunction (ugh!!!)

[TODO]

## Negation (ugh!!!)

[TODO]

# Debugging

("Computer says 'no'")

# The art of cheating without being caught

## Barliman interpreter hax

[TODO]

# Data structures

## Pairs and lists

[TODO]

## Sets and CLP(Set)

[TODO]

## ADTs

[TODO]

## records

[TODO]

# Program synthesis

## e-graphs, VSA, tree autamata

[TODO]

# Semantics of logic programming

[TODO]

# Tabled evaluation

[TODO]

# Term rewriting and term reduction

## Confluence and Church-Rosser

### Modified notion for Verse Calculus

[TODO]

## Knuth-Bendix completion

[TODO]

## Linear logic multiset rewriting

[TODO]

# Things I'm excited about right now

## machine learning for automated theorem proving and proof assistants, inspired by Alpha Go [add CPP'24 talk] [implement this!!!!]

[TODO]

## Natural deduction [implement this!!!!]

[TODO]

## Sequent calculus [add tutorial]

[TODO]

## Incorrectness logics

[TODO]

## Using sequent calculus to implement a type system proving an expression won't evaluate [TODO <- add POPL'24 reference] [implement this!!!!]

[TODO]

# Interesting things I know almost nothing about, but which seem relevant

## monadic second-order logic

[TODO]

# What does `conde` stand for?  Where did it come from?  Why does it resemble Scheme's `cond`?

[TODO]

# What is environment trimming?  Does miniKanren implement environment trimming?

[TODO]

# Is there an abstract machine for miniKanren?

[TODO]

# Is there a formal semantics for miniKanren?

[TODO]