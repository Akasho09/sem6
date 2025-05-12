## Design the SDD for generating syntax tree for Arithmetic Statements. Also, using this SDD, construct the syntax tree for the expression:   a = (b - 2) / (b + c^3)

E->E1=T (E.ptr = new Node ('=' , E1.ptr , T.ptr) )

![akash](<Screenshot 2025-04-08 at 7.59.03 PM.png>)

## binary to decimal with fraction 
![alt text](<Screenshot 2025-04-08 at 8.03.32 PM.png>)

## storing type info into symbol table using SDD
![alt text](<Screenshot 2025-04-08 at 10.11.00 PM.png>)

## TAC uisnd SDD 
![alt text](<Screenshot 2025-04-08 at 10.23.39 PM.png>)

## 🔹 Answer 3a: Types of Attributes
Attributes in syntax-directed translation are used to define semantics. Two major types:

1. Synthesized Attributes
Computed from children to parent in the parse tree.
Suitable for bottom-up parsing.
Example: For expression E → E1 + T,
E.val = E1.val + T.val

2. Inherited Attributes
Passed from parent or siblings to children.
Used in top-down parsing or for passing context.
Example: T → (E) with attribute E.inh = T.inh

| Aspect           | Synthesized            | Inherited               |
| ---------------- | ---------------------- | ----------------------- |
| Direction        | Bottom-up              | Top-down or lateral     |
| Evaluation Order | Post-order (DFS)       | Pre-order or contextual |
| Use Case         | Arithmetic Expressions | Type propagation        |

