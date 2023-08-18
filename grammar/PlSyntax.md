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

## Example

```
program ::= {statement}
statement ::= "PRINT" (expression | string) nl
    | "IF" comparison "THEN" nl {statement} "ENDIF" nl
    | "WHILE" comparison "REPEAT" nl {statement} "ENDWHILE" nl
    | "LABEL" ident nl
    | "GOTO" ident nl
    | "LET" ident "=" expression nl
    | "INPUT" ident nl
comparison ::= expression (("==" | "!=" | ">" | ">=" | "<" | "<=") expression)+
expression ::= term {( "-" | "+" ) term}
term ::= unary {( "/" | "*" ) unary}
unary ::= ["+" | "-" | "!"] unary | primary
primary ::= number | ident
nl ::= '\n'+
```

If you'd like to know a bit more about this notation... {} means zero or more, [] means zero or one, + means one or more of whatever is to the left, () is just for grouping, and | is a logical or. Words are either references to other grammar rules or to tokens that we have already defined in our lexer. I denote keywords and operators as quoted strings of text.

To achieve different levels of precedence, we organize the grammar rules sequentially. Operators with higher precedence need to be "lower" in the grammar, such that they are lower in the parse tree. The operators closest to the tokens in the parse tree (i.e., closest to the leaves of the tree) will have the highest precedence. Another way to think about it is how tightly the operators bind to the operands. When parsing, if there is not an operator at a given level, then it passes through to the next level and creates a node in the tree with only one child.

#### Adding new rule

Let’s modify the grammar to support expressions inside parentheses.
```
primary ::= number | ident | LPAREN expression RPAREN
```

LPAREN represents a left parenthesis ‘(‘, the terminal RPAREN represents a right parenthesis ‘)’

Here is an interesting feature of our new grammar - it is [recursive](https://en.wikipedia.org/wiki/Recursive_descent_parser). If you try to derive the expression 2 * (7 + 3), you will start with the expr start symbol and eventually you will get to a point where you will recursively use the expr rule again to derive the (7 + 3) portion of the original arithmetic expression.

Recursion in the grammar is a good sign that the language being defined is context-free instead of regular. In particular, recursion where the recursive nonterminal has productions on both sides implies that the language is not regular.
