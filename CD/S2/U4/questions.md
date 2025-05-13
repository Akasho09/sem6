## Generate the short circuit TAC for the following sample:
---
Step 1: Translate the condition using short-circuit evaluation
Condition: ((a > b && c > d) || e < f)

t1 = a > b
ifFalse t1 goto L1
t2 = c > d
ifFalse t2 goto L1
goto L2
L1: t3 = e < f
ifFalse t3 goto L6 ← (exit condition)
L2: // loop body starts here

Step 2: Loop Body Translation
t4 = a + e
t5 = t4 / 2
n = t5
i = 0
L3: if i >= n goto L5
t6 = b / c
t7 = t6 * t6
t8 = a + t7
a = t8
i = i + 1
goto L3
L5: goto #00 (back to while condition check)

## List the various three address code statements with suitable syntax and examples. Also evaluate the advantages of generating intermediate code in a compiler.
---
### 🔹 Types of TAC (Three Address Code) Statements:
1. Assignment
x = y op z
Example: a = b + c

2. Unary Operation
x = op y
Example: a = -b

3. Copy Statement
x = y
Example: a = b

4. Unconditional Jump
goto L
Example: goto L1

5. Conditional Jump
if x relop y goto L
Example: if a > b goto L2

6. Label Definition
L:
Example: L1:

7. Array Access
x = y[i] or x[i] = y
Example: a = arr[i]

8. Pointer Assignment
x = *y or *x = y
Example: a = *ptr

9. Procedure Call and Return
call proc, n or return x
Example: call sum, 2

### 🔹 Advantages of Using Intermediate Code (TAC):
1. Machine Independence:
It allows separation of front-end (syntax) and back-end (machine-specific) phases.

2. Optimization:
Easier to apply code optimization techniques on intermediate code.

3. Portability:
Intermediate code can be reused across multiple target architectures.

4. Simplifies Code Generation:
Helps in modular compiler design.

5. Error Handling:
Errors can be detected early before final machine code is generated.

