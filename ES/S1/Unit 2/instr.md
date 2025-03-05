Data Transfer Instructions

- MOV A, Rn → Move register Rn to accumulator.
mov @r1 , a == move to memory pointefd by r1 .
- MOV A, direct → Move direct address content to accumulator.
- MOVX A, @DPTR → Move external data memory content to accumulator.
PUSH direct → Push content to stack.
POP direct → Pop content from stack.

Arithmetic Instructions.
ADD A, Rn → Add register Rn to accumulator
SUBB A, direct → Subtract direct address content from A with borrow
MUL AB → Multiply A and B (16-bit result in A and B)
DIV AB → Divide A by B (A = quotient, B = remainder)


Logical Instructions
ANL A, Rn → AND operation between A and register Rn
ORL A, direct → OR operation between A and direct address content
XRL A, #data → XOR immediate data with A
CPL A → Complement accumulator
INC Rx – Increment the contents of register Rx by 1
DEC Rx – Decrement the contents of register Rx by 1
DJNZ Rn, label - DJNZ (Decrement and Jump if Not Zero)

Branching (Jump & Call) Instructions
SJMP label → Short jump (within ±127 bytes)
LJMP address → Long jump (16-bit address)
AJMP address → Absolute jump (11-bit address)
JZ label → Jump if A is zero
JNZ label → Jump if A is nonzero
CALL address → Call subroutine at given address
RET → Return from subroutine

Bit Manipulation Instructions
- SETB C → Set carry flag
  SETB P0.7  ===> SET 87H , 1 is 90.
- CLR C → Clear carry flag
CPL C → Complement carry flag
- JB bit, label → Jump if bit is set
acc.7
- JNB bit, label → Jump if bit is not set