# Knowledge Base: Compilers

## Getting Started
1. [Let's make a Teeny Tiny compiler](https://austinhenley.com/blog/teenytinycompiler1.html)
2. [Let’s Build A Simple Interpreter](https://ruslanspivak.com/lsbasi-part1/)
3. [ A Compiler Writing Journey ](https://github.com/DoctorWkt/acwj)
4. [Basics of Compiler Design](http://hjemmesider.diku.dk/~torbenm/Basics/) - basic concepts
5. [Crafting Interpreters](http://www.craftinginterpreters.com/) - most valuable resource by far for me
6. [Awesome resources on Compilers, Interpreters and Runtimes](https://github.com/aalhour/awesome-compilers)

## Parsing
[Recursive descent parser](https://en.wikipedia.org/wiki/Recursive_descent_parser)

[Operator-precedence_parser](https://en.wikipedia.org/wiki/Operator-precedence_parser)

[Pratt-parsers-expression-parsing-made-easy](https://journal.stuffwithstuff.com/2011/03/19/pratt-parsers-expression-parsing-made-easy/)

### Parse Trees and AST

[Grammatically Rooting Oneself With Parse Trees](https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff)

[Leveling Up One’s Parsing Game With ASTs](https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff)

[Abstract vs. Concrete Syntax Trees](https://eli.thegreenplace.net/2009/02/16/abstract-vs-concrete-syntax-trees)

[Simple but Powerful Pratt Parsing](https://matklad.github.io/2020/04/13/simple-but-powerful-pratt-parsing.html#Simple-but-Powerful-Pratt-Parsing)

### Auxiliary

BNF converter?? - http://bnfc.digitalgrammars.com/

Visitor pattern can be usefull when traversing AST - https://refactoring.guru/design-patterns/visitor

## General

https://orangejuiceliberationfront.com/how-to-write-a-compiler/

https://www.hanshq.net/ones-and-zeros.html

https://meta.stackexchange.com/questions/25840/can-we-stop-recommending-the-dragon-book-please

Structure and
Interpretation
of Computer
Programs (Book)

https://github.com/maiquynhtruong/compilers/wiki

https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html

https://archive.org/details/ComputerSystems/Eng/page/n5/mode/2up

[Resources for Amateur Compiler Writers](https://c9x.me/compile/bib/)

https://medium.com/free-code-camp/the-programming-language-pipeline-91d3f449c919

https://tomassetti.me/resources-create-programming-languages/

[Let's Build a Compiler](https://compilers.iecc.com/crenshaw/)

[implementing-type-inference](https://stackoverflow.com/questions/415532/implementing-type-inference)

[Anders Hejlsberg on Modern Compiler Construction](https://learn.microsoft.com/en-us/shows/seth-juarez/anders-hejlsberg-on-modern-compiler-construction)

## Program Analysis

https://pwn.umasscybersec.org/lectures/#

https://www.youtube.com/watch?v=te2iYyZfckg&list=PLC-dUCVQghfdu7AG5f_p4oRyKgjDuoAWU

https://github.com/seal9055/resources?tab=readme-ov-file#program-analysis

Principles of Program Analysis (Textbook)

- Data Flow Analysis: Theory and Practice (Textbook)

- Value-Range Analysis of C Programs: Towards Proving the Absence of Buffer
Overflow Vulnerabilities (Textbook)

University of Pennsylvania Course
https://www.youtube.com/playlist?list=PLF3-CvSRq2SYXEiS80KuZQ80q8K2
aHLQX

University of Stuttgart Course
https://www.youtube.com/playlist?list=PLBmY8PAxzwIEGtnJiucyGAnwWpxA
CE633

https://edmcman.github.io/papers/oakland10.pdf

## Theory to look at

automata theory

graph-coloring

register-spill algorithms

peephole optimizations.

Look for more at: https://lowlevelbits.org/how-to-learn-compilers-llvm-edition/ (Theory section)

## LLVM

- [A Gentle Introduction to LLVM IR](https://mcyoung.xyz/2023/08/01/llvm-ir/)

- https://blog.regehr.org/

- [Fuzzer](https://github.com/llvm-mirror/llvm/tree/release_39/lib/Fuzzer): this is [libFuzzer](http://llvm.org/docs/LibFuzzer.html), a coverage-guided fuzzer similar to [AFL](http://lcamtuf.coredump.cx/afl/). It doesn’t fuzz LLVM components, but rather uses LLVM functionality in order to perform fuzzing of programs that are compiled using LLVM.

