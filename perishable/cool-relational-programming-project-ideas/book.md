% Cool Relational Programming Project Ideas
% William E. Byrd
% April 1, 2024

Copyright 2024 by William E. Byrd

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). (CC BY 4.0) 

# What is this book?

[TODO]

# Why this book?

[TODO]

# The writing philosophy behind this book

[TODO]

# Who is the audience for this book?

[TODO]

# Cool Relational Programming Project Ideas

## Relational Prolog interpreter

It is a pain to translate Prolog programs to miniKanren, especially since Prolog programs tend to contain a mixture of pure and impure logical operations.  Sidestep the issue by just implementing an interpreter for Prolog, cuts and all, as a miniKanren relation.  Ideally would support `copy_term`, `!` (cut), `call`, etc.  Stage the interpreter for improved performance in some cases.

This interpreter would, in some ways, be similar in spirit to mk-in-mk.  You'd be able to do many of the same types of synthesis problems.

This interpreter would also explore how the "relational interpreter" encoding can be used to deal with impure operations, or operations that are tricky or awkware or error-prone to encode relationally in pure miniKanren.  For example, one way to translate Scheme's `cond` or Scheme's `not` or pattern matching to the miniKanren setting is to just write a relational Scheme interpreter that includes those operations.  Similarly, one way to deal with the impure operators in Prolog would be to just run the impure Prolog program in a pure implementation of a Prolog interpreter in miniKanren.

## Prolog -> miniKanren compiler

Write a compiler for Prolog, including impure operations, to miniKanren, using only pure relational miniKanren operations.

Could also write a compiler that compiles to mk with impure operations like `conda`, `condu`, `project`, etc.  A person could then hand-massage the resulting impure mk program to make it as relational as desired.

Both compilers could be useful and interesting, although of course I strongly prefer the first version!

## Create a catalog of Prolog-to-miniKanren transformations, including for impure Prolog operations/idioms to pure miniKanren operations/idioms.

Similar to correctness-preserving transformations that Dan Friedman teaches in C311, but for turning nasty impure Prolog code into beautiful relations mk code!  :P
