## 🔷 What is GENCODE?
- GENCODE is a code generation algorithm used in compilers to translate intermediate representation (like TAC) into target code (like assembly/machine code).

It handles:
1. Instruction selection
1. Register allocation
1. Instruction ordering

### 🔷 Internal Cases in GENCODE
- GENCODE works on a tree (or DAG) structure of an expression and handles different operations:
    1. Leaf nodes: Generate code to load variables/constants into registers.
    1. Binary operations: Generate instructions for arithmetic (add, sub, mul, div).
    1. Temporary reuse: Avoid redundant operations if a value is already computed.
    1. Assignment: Store result back to memory or a variable.

### example
1  t1 = b + a  
2  t2 = c - d  
3  t3 = t1 * t2  
4  t4 = t3 / 2  
5  a  = t4

1. ▶️ Step 1: t1 = b + a
MOV R1, b
ADD R1, a
Result in R1 → t1

2. ▶️ Step 2: t2 = c - d
MOV R2, c
SUB R2, d
Result in R2 → t2

3. ▶️ Step 3: t3 = t1 * t2
MUL R3, R1, R2
Result in R3 → t3

4. ▶️ Step 4: t4 = t3 / 2
MOV R4, R3
DIV R4, 2
Result in R4 → t4

5. ▶️ Step 5: a = t4
MOV a, R4
Store final result to variable a

- ✅ Final Generated Target Code:
```java
MOV R1, b
ADD R1, a       ; R1 = t1

MOV R2, c
SUB R2, d       ; R2 = t2

MUL R3, R1, R2  ; R3 = t3

MOV R4, R3
DIV R4, 2       ; R4 = t4

MOV a, R4       ; a = t4
```

