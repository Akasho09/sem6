## Parsing approaches. 
Top-down Parsing: LL (1) Parsing, 
Bottom Up Parsing technique, LR(1) Parsing, SLR parsing, Canonical LR Parsing, LALR Parsing,
Error recovery strategies, Yacc: an LALR(1) Parser generator


## Top-Down Parsing: LL(1) Parsing
- Starts from the start symbol of the grammar and tries to derive the input string by expanding the productions.
Uses a predictive approach, meaning it chooses the correct production based on lookahead.
- Common methods include Recursive Descent Parsing and LL(1) Parsing.

1. Recursive Descent Parser :
A recursive descent parser is a top-down parser that processes input based on a set of recursive functions, where each function corresponds to a grammar rule. It parses the input from left to right, constructing a parse tree by matching the grammar’s production rules. 
This parser is simple to implement and is suitable for LL(1) grammars, where decisions can be made based on a single lookahead token. While straightforward, recursive descent parsers struggle with left-recursive grammars and may require grammar transformations to handle such cases effectively.
![alt text](<Screenshot 2025-02-28 at 3.19.31 PM.png>)


2. Follow and first :
- First Set: The First set of a non-terminal contains all the terminal symbols that can appear at the beginning of any string derived from that non-terminal. In other words, it tells us which terminal symbols are possible when expanding a non-terminal.
- Follow Set: The Follow set of a non-terminal contains all the terminal symbols that can appear immediately after that non-terminal in any derivation. It helps identify what can follow a non-terminal in the grammar and is essential for handling productions where a non-terminal is at the end of a rule.

![alt text](<Screenshot 2025-02-28 at 3.43.29 PM.png>)
![alt text](<Screenshot 2025-02-28 at 3.53.49 PM.png>)
![alt text](<Screenshot 2025-02-28 at 3.59.55 PM.png>)