## X → XAa | y  
   A → Az | Ad | w
---

1. ✅ Step 1: Check for Left Recursion
2. 🔧 Step 2: Eliminate Left Recursion
ie    A->Az|w
    => A->wz*
    => A->wA'
    & A'->zA'|epsilon.
3. ✅ Step 3: Updated Grammar (No Left Recursion)
X  → y X'  
X' → Aa X' | ε  
A  → w A'  
A' → z A' | d A' | ε

- Now apply LL1 

## S → id = E | print(L)  
    E → id | num | E + E | (S, E)  
    L → E | L, E
---
### 🔹 FIRST Sets
- FIRST(id) = {id}

- FIRST(num) = {num}

- FIRST(E)
    E → id → id
    E → num → num
    E → E + E → depends on FIRST(E), so needs recursion
    E → (S, E) → starts with (
> ⇒ FIRST(E) = {id, num, (}

- FIRST(S)
    S → id = E → id
    S → print(L) → print
> ⇒ FIRST(S) = {id, print}

- FIRST(L)
    L → E → {id, num, (}
    L → L, E → needs FIRST(L)
> ⇒ FIRST(L) = {id, num, (}

### 🔹 FOLLOW Sets
Let’s assume S is the start symbol → $ ∈ FOLLOW(S)
1. From S → id = E, FOLLOW(E) includes FOLLOW(S) = {$}
2. From S → print(L) → FOLLOW(L) = {`} (right parenthesis)

From E → (S, E) → S is followed by , → FOLLOW(S) ⊇ {,}

E followed by ) → FOLLOW(E) ⊇ {)}

L → L, E → FOLLOW(L) ⊇ {,}

L → E → FOLLOW(E) ⊇ FOLLOW(L)

Final sets:

FOLLOW(S) = {,, )} (due to (S, E))

FOLLOW(E) = {,, ), $}

FOLLOW(L) = {)}


## ✅ Q No. 2b: LR(1) Parser Structure & Rightmost Derivation

### LR(1) Parser Structure:
LR(1) parser uses:
A stack (to store states/symbols)
An input buffer (for lookahead)
An action/goto table
Items are of the form [A → α • β, a], where a is the lookahead.

### 🔹 Why Rightmost Derivation in Reverse?
- LR parsers build the parse tree bottom-up
- They reduce the rightmost production first
- But parsing happens from left to right
Therefore, it’s rightmost derivation in reverse, constructing the derivation steps backwards

## ✅ Q No. 2c: Determine if CFG is LL(1), SLR(1), CLR(1)
S → AA  
A → aSa | a
1. 🔹 Let's test LL(1):
Check if A → aSa | a is ambiguous in FIRST sets:
- Both derive from 'a' → FIRST sets overlap
- Union of FIRSTs isnt empty set. 
So: ❌ Not LL(1)

2. 🔹 Now test SLR(1):
Check for reduce/reduce conflict or shift/reduce conflict using FOLLOW sets.
Let's assume:
FOLLOW(A) includes a and $
Both productions start with a, and the parser may be unable to distinguish between aSa and a after seeing a
→ SLR(1) might still conflict on a

3. 🔹 Test CLR(1):
LR(1) items include lookahead, which helps distinguish between the two rules of A → aSa | a.
→ Using the lookahead symbol (1-token of lookahead), parser can decide whether to reduce to a or continue with aSa
✅ So: This grammar is CLR(1)


