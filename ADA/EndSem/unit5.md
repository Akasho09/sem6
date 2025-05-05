## 

## Naive Algo : 
Given text string with length n and a pattern with length m, the task is to prints all occurrences of pattern in text.
- Slide the pattern over text one by one and check for a match. If a match is found, then slide by 1 again to check for subsequent matches. 
- COMPLEXITY = O(n+m-1)(m)


## Robin Karp algo : 
- Step 1: Choose a suitable base and a modulus:
Select a prime number ‘p‘ as the modulus. This choice helps avoid overflow issues and ensures a good distribution of hash values.
Choose a base ‘b‘ (usually a prime number as well), which is often the size of the character set (e.g., 256 for ASCII characters).


- Step 2: Initialize the hash value:
Set an initial hash value ‘hash‘ to 0.

- Step 3: Calculate the initial hash value for the pattern:
Iterate over each character in the pattern from left to right.
For each character ‘c’ at position ‘i’, calculate its contribution to the hash value as ‘c * (bpattern_length – i – 1) % p’ and add it to ‘hash‘.
This gives you the hash value for the entire pattern.

- Step 4: Slide the pattern over the text:
Start by calculating the hash value for the first substring of the text that is the same length as the pattern.

- Step 5: Update the hash value for each subsequent substring:
To slide the pattern one position to the right, you remove the contribution of the leftmost character and add the contribution of the new character on the right.
The formula for updating the hash value when moving from position ‘i’ to ‘i+1’ is:
hash = (hash – (text[i – pattern_length] * (bpattern_length – 1)) % p) * b + text[i]

- Step 6: Compare hash values:
When the hash value of a substring in the text matches the hash value of the pattern, it’s a potential match.
If the hash values match, we should perform a character-by-character comparison to confirm the match, as hash collisions can occur.

### Time Complexity: 

- The average and best-case running time of the Rabin-Karp algorithm is O(n+m), but its worst-case time is O(nm).
- The worst case of the Rabin-Karp algorithm occurs when all characters of pattern and text are the same as the hash values of all the substrings of T[] match with the hash value of P[]. 


## string matching using finite automata
-  This approach examines each character of text exactly once to find the pattern. Thus it takes linear time for matching but preprocessing time may be large.
- It is defined by tuple M = {Q, Σ, q, F, d} Where Q = Set of States in finite automata
    - Q = Set of States in finite automata
    
    - Σ=Sets of input symbols

    - q. = Initial state

    - F = Final State

    - σ = Transition function

> Time Complexity of finite automata = O(M³|Σ|).
> Time complexity of string matching using finite automata = O(M³|Σ|+n) = O(n).
