## Parsing approaches. 

Top-down Parsing: LL (1) Parsing, 

Bottom Up Parsing technique, LR(1) Parsing, SLR parsing, Canonical LR Parsing, LALR Parsing,

Error recovery strategies, Yacc: an LALR(1) Parser generator

## Top-Down Parsing:

- Starts from the start symbol of the grammar and tries to derive the input string by expanding the productions.

Uses a predictive approach, meaning it chooses the correct production based on lookahead.

- Common methods include Recursive Descent Parsing and LL(1) Parsing.

1. `Recursive Descent Parser` :

A recursive descent parser is a top-down parser that processes input based on a set of recursive functions, where each function corresponds to a grammar rule. It parses the input from left to right, constructing a parse tree by matching the grammar’s production rules. 

This parser is simple to implement and is suitable for LL(1) grammars, where decisions can be made based on a single lookahead token. While straightforward, recursive descent parsers struggle with left-recursive grammars and may require grammar transformations to handle such cases effectively.

![alt text](<Screenshot 2025-02-28 at 3.19.31 PM.png>)

### Follow and first :

- First Set: The First set of a non-terminal contains all the terminal symbols that can appear at the beginning of any string derived from that non-terminal. In other words, it tells us which terminal symbols are possible when expanding a non-terminal.
- Follow Set: The Follow set of a non-terminal contains all the terminal symbols that can appear immediately after that non-terminal in any derivation. It helps identify what can follow a non-terminal in the grammar and is essential for handling productions where a non-terminal is at the end of a rule.

![alt text](<Screenshot 2025-02-28 at 3.43.29 PM.png>)

![alt text](<Screenshot 2025-02-28 at 3.53.49 PM.png>)

![alt text](<Screenshot 2025-02-28 at 3.59.55 PM.png>)

2. `Non Recursive Descent Parser` : or LL1  or predictive parse table 
An LL(1) parser is a top-down parsing technique that processes input from Left to right (L), constructs a Leftmost derivation (L), and uses 1 symbol of lookahead (1).
- Properties of LL(1) Parsing
✅ Top-Down Parsing – Starts from the start symbol and expands productions.
✅ Predictive Parsing – Uses a parsing table to decide which rule to apply.
✅ Non-Backtracking – No need to backtrack if the grammar is LL(1).
✅ Requires LL(1) Grammar – The grammar must not have left recursion or ambiguity.

## Bottom-up parsing 
is a type of syntax analysis method where the parser starts from the input symbols (tokens) and attempts to reduce them to the start symbol of the grammar (usually denoted as S). The process involves applying production rules in reverse, starting from the leaves of the parse tree and working upwards toward the root.
![alt text](image.png)

1. LR Parsing
LR parsing is a type of bottom-up parsing technique used to handle large and complex grammars. It is commonly used in compilers for programming languages. The name “LR” comes from two parts:

The “L” stands for left-to-right scanning of the input. This means the parser reads the input string one symbol at a time, from left to right.

The “R” stands for rightmost derivation in reverse. This refers to the way the parser constructs the parse tree. Instead of building the tree from the top down (like in top-down parsing), LR parsing works from the leaves (the input symbols) and gradually reduces them back to the start symbol, following a rightmost derivation in reverse.

