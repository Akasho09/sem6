 **Lexical analyzer**: 
- LA or Scanners reads the source program one character at a time, carving the source program into a
sequence of automic units called tokens.
-  operators , identifiers , constants , speacial symols 
- eliminates coment lines, blank spaces  from code .
- gives col, row no of error messages .
- code continues to compile even if error to give all errors 
![alt text](<../../../Screenshot 2025-02-27 at 6.46.43 PM.png>)

> A lexeme is the actual sequence of characters that forms a meaningful unit in a programming language.
Example: In the statement int num = 5;, the lexemes are:
"int" (keyword)
"num" (identifier)
"=" (assignment operator)
"5" (integer literal)
";" (delimiter)
Token

> A token is the classification or category of lexemes.
It represents a general type rather than a specific string.
Example: The lexemes from the statement above belong to the following tokens:
"int" → KEYWORD
"num" → IDENTIFIER
"=" → ASSIGNMENT_OPERATOR
"5" → NUMBER
";" → SEMICOLON
Pattern

> A pattern is a rule or regular expression that defines the structure of lexemes belonging to a specific token.
Example patterns:
IDENTIFIER: [a-zA-Z_][a-zA-Z0-9_]* (matches variable names)
NUMBER: [0-9]+ (matches integer literals)
KEYWORD: A fixed set of words like int, if, return, etc.