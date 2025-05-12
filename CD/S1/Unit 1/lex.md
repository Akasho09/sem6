# Lexical analyzer :
- The Lexical Analyzer (also known as a scanner) is the first phase of a compiler. 
- It reads the source code character by character, groups them into tokens, and sends these tokens to the syntax analyzer.

## Main Responsibilities of Lexical Analyzer
1. Tokenization
- Breaks the input source code into tokens, which are the smallest meaningful units (e.g., keywords, identifiers, operators, literals, punctuation).

2. Removing White Spaces and Comments
- Ignores blanks, tabs, newlines, and comments which are not meaningful for syntax analysis.

3. Symbol Table Create and Management
- Adds new identifiers (like variable names) into the symbol table.
    - A Symbol Table is a data structure used by a compiler to store information about identifiers (like variable names, function names, classes, objects, etc.) in a source program.
    - It acts like a dictionary that allows the compiler to keep track of what each symbol means, its type, scope, memory location, and other attributes.
    - MAINLY USES Hash Table DS .

4. Error Detection
- Reports lexical errors, such as illegal characters or malformed identifiers.
- Error Handling is very localized, with Respect to Input Source eg while(x:=0) generates no erros here . 

5. Send Tokens to Parser

### Input Buffering 
- To ensure that a right lexeme is found, one or more characters have to be looked up beyond the next lexeme. Hence a two-buffer scheme is introduced to handle large lookaheads safely.
- Input buffering helps the lexical analyzer process input efficiently by reducing file I/O and allowing easy backtracking and lookahead. The two-buffer scheme is the standard method for achieving this.
- The lexical analyzer scans the input from left to right one character at a time. 
- It uses two pointers begin ptr(bp) and forward ptr(fp) to keep track of the pointer of the input scanned.move forward till we get the longest matching lexeme and register the lexeme to the token in symbol table .

> buffer  : using memory to temporarily store data, particularly input, while it's being processed

- LA or Scanners reads the source program one character at a time, carving the source program into a sequence of automic units called `tokens`.
-  operators , identifiers , constants , speacial symols. 
- eliminates comment lines, blank spaces  from code .
- gives col, row no of error messages .
- code continues to compile even if error to give all errors 

## count lexemes 
- longest matching 
- "akssh" = 1 lexeme .
![alt text](<Screenshot 2025-02-27 at 6.46.43 PM.png>)


### A lexeme 
is the actual sequence of characters that forms a meaningful unit in a programming language.
Example: In the statement int num = 5;, the lexemes are:
"int" (keyword)
"num" (identifier)
"=" (assignment operator)
"5" (integer literal)
";" (delimiter)

### Token
> A token is the classification or category of lexemes.
It represents a general type rather than a specific string.
Example: The lexemes from the statement above belong to the following tokens:
"int" → KEYWORD
"num" → IDENTIFIER
"=" → ASSIGNMENT_OPERATOR
"5" → NUMBER
";" → SEMICOLON

### Pattern
> A pattern is a rule or regular expression that defines the structure of lexemes belonging to a specific token.
- pattern is of tokens .
Example patterns:
IDENTIFIER: [a-zA-Z_][a-zA-Z0-9_]* (matches variable names)
NUMBER: [0-9]+ (matches integer literals)
KEYWORD: A fixed set of words like int, if, return, etc.


## terminnology :
1. Prefix:
A prefix of a string is a contiguous sequence of characters starting from the beginning of the string.
- Example: For the string "ABC", the prefixes are:
"" (empty string), "A", "AB", "ABC".
A string of length n has n+1 prefixes.

2. Suffix:
A suffix of a string is a contiguous sequence of characters starting from the end of the string.
- Example: For the string "ABC", the suffixes are:
"", "C", "BC", "ABC".
A string of length n has n+1 suffixes.

3. Substring:
A substring is any contiguous sequence of characters within a string.
- Example: For "ABC", the substrings are:
"", "A", "B", "C", "AB", "BC", "ABC".
A string of length n has n(n+1)/2 substrings.

4. Subsequence:
A subsequence is a sequence that can be derived by deleting some characters from the string without changing the relative order of the remaining characters.
- Example: For "ABC", some subsequences are:
"", "A", "B", "C", "AB", "AC", "BC", "ABC".
- A string of length n has 2^n subsequences.
Count of These Elements in a Process String of Size n:
> Prefixes: n + 1
> Suffixes: n + 1
> Substrings: n(n + 1) / 2
> Subsequences: 2^n