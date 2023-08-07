# Programmming language syntax

Programmming languages needs a grammar. This is a formal way to describe all of the code that is legal in Programmming language. 
If you've ever had a compiler yell at you about a syntax error, it is because your code did not follow the language's grammar.

https://en.wikipedia.org/wiki/Syntax_(programming_languages)

```
Start with expressions and operators, work upwards to statements, then to functions/classes etc. Keep a list of what punctuation is used for what.

In parallel define syntax for referring to variables, arrays, hashes, number literals, string literals, other builtin literal. Also in parallel define your data naming model and scoping rules.

To check whether your grammar makes sense focus on a level (literal/variable, operator, expression, statement, function etc) and make sure that punctuation and tokens from other levels interspersed or appended/prepended is not gonna cause an ambiguity.

Finally write it all out in EBNF and run it through ANTLR or similar.

Also best not to reinvent the wheel. I normally start off by choosing sequences to start and end statement blocks and functions, and mathematical operators, that are usually fundamentally C-like, ECMAScript-like, Basic-like, command-list based or XML-based. This helps a lot cos this is what people are used to working with.

Of course you have to come up with a pretty compelling reason not to abandon writing a new language and just stick with C, ECMAScript, or Basic which are well tested and much used.

I've often started defining new language only to find someone else has already implemented a feature somewhere in some existing language.

If your goal is speed of development for some specific project, you might be better off prototyping in something like Python, Lua or SpiderMonkey if you're looking to get up and running quickly and want to reduce the amount of typing necessary in most compiled languages.
```

https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form

https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form

