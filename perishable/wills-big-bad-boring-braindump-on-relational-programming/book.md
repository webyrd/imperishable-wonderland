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

Get it done!  "Write poorly, proudly!" [TODO <- something like that --- find exact quote in the Film Courage video I linked to in a recent video; add reference]  Get all the ideas in my head down on paper as quickly as possible.  "The worst finished book is better than the best unfinished book" [TODO <- something like that --- find exact quote in the Film Courage video I linked to in a recent video; add reference]

Dean Wesley Smith's notion of working at "pulp speed" also inspires me to write a book "into the dark" [TODO <- something like that --- find exact phrase in DWS book; add reference]  Just sit down and start typing!

# Who is the audience for this book?

People who are trying to learn about miniKanren and/or relational programming and/or constraint logic programming, etc., at a deeper level than can be found in 'The Reasoned Schemer' or the original microKanren paper.  If nothing else, I hope you will find your own connections and inspiration in this semi-random collection of relational programming lore.  You are almost guaranteed to stumble across some ideas or techniques or artifacts or perspectives that you haven't seen before, even if you have been programming for a very long time.

# What is relational programming?

Relational programming is a programming paradigm in which computations are modeled as mathematical (or logical) relations.  This is in constrast, for example, to functional programming, in which computations are modeled as mathematical functions, mapping inputs to outputs.  Unlike most approached to programming, relational programming dispenses with the notions of inputs and outputs.  Instead, a relations takes zero or more *terms*, and each term can contain zero or more *logic variables* (also known as *unification variables*) that can represent unknown values.  Relational programs *constrain* these terms (including the logic variables in these terms) using *constraints*, such as *syntactic equality* and *syntactic disequality*.  A constraint logic reasoning engine performs a (potentially very sophisticated) mixture of constraint solving and search in an attempt to find assignments to the logic variables that satisfy all the constraints.  If the relational program includes recursion, there may be multiple solutions to one of these constraint problems, including infinitely many solutions.  Alternatively, the constraint logic engine might search an infinite search space looking for a non-existent solution to a constraint problem; in this case, the constraint logic engine may end up *diverging* (looping foreer), or may able to prove in finite time that no solution exist (*finite failure*).

# What is miniKanren?

miniKanren is a family of constraint logic programming languages, each of which is implemented by one or more constraint logic reasoning engines.  Many implementation of miniKanren focus on logical purity, emphasizing the relational aspects of computation.  Some variants of miniKanren-like languages, such as core.logic in Clojure, focus more on pragmatic uses of the language, as part of the program logic in a "standard" application.  Other variants, such as OCanren in OCaml, explore the relational aspects from a research perspective.

Most miniKanrens are implemented as *embedded domain-specific languages* (EDSLs), meaning that they extend some *host language* with additional functions, methods, etc., supporting the miniKanren language, along with an implementation in the host language of a constraint logic reasoning engine.  Historically miniKanren has been implemented in variants of Lisp (for example, Scheme, Racket, and Clojure) or other functional languages (OCaml and Haskell).  There has also been some work on implementing miniKanren as a stand-along language and run-time.

# Truth versus success

