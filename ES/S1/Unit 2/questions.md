## 
ORG     0000H          ; Origin at address 0000H
SJMP    START          ; Jump to start of the program

ORG     400H           ; Origin for data in ROM
DATA:   DB 58H, 3EH, 8FH, 4EH, 98H, 4FH  ; Sample Data in ROM

ORG     0100H          ; Origin at address 0100H for the program instructions
START:  MOV DPTR, #0400H  ; Initialize DPTR to point to the ROM data starting 0400H
        MOV R0, #50H     ; Initialize R0 to point to the RAM location 50H (positive data storage)
        MOV R1, #60H     ; Initialize R1 to point to the RAM location 60H (negative data storage)
        MOV R2, #06      ; Initialize counter R2 with the number of data bytes (6 in this case)

CHECK:  MOVX A, @DPTR   ; Move data from external memory pointed by DPTR to A
        JNB ACC.7, POSITIVE  ; Check the MSB (bit 7) of A to determine if the number is positive (JNB: Jump if No Bit set)
        
NEGATIVE: MOV @R1, A    ; If the number is negative, store in location pointed by R1
        INC R1          ; Increment R1 to point to the next location for negative data
        SJMP NEXT       ; Jump to next iteration
        
POSITIVE: MOV @R0, A    ; If the number is positive, store in location pointed by R0
        INC R0          ; Increment R0 to point to the next location for positive data

NEXT:   INC DPTR        ; Increment DPTR to point to the next data byte
        DJNZ R2, CHECK  ; Decrement R2 and jump to CHECK if R2 is not zero

END:    SJMP END        ; End of the program. Loop indefinitely.

END


---
ORG     0000H           ; Origin at address 0000H
SJMP    START           ; Jump to start of the program

ORG     0400H           ; Data stored in ROM
DATA:   DB 58H, 3EH, 8FH, 4EH, 98H, 4FH, 7AH, 2BH, 9CH, 1DH, 0EH, 6FH, 8AH, 0BH, 5CH
                        ; Sample data (15 bytes)

ORG     0100H           ; Start of program execution
START:
        MOV DPTR, #0400H    ; Point DPTR to ROM (0400H)
        MOV R0, #60H        ; RAM address for storing positive numbers
        MOV R1, #90H        ; RAM address for storing negative numbers
        MOV R2, #0FH        ; Counter for number of values (15)

PROCESS:
        MOVC A, @DPTR     ; Fetch data from ROM into A
        INC DPTR            ; Increment DPTR to point to next data byte
        JB  ACC.7, NEGATIVE ; If MSB is 1, number is negative; jump to NEGATIVE

POSITIVE:
        MOV @R0, A          ; Store positive number at RAM (60H onwards)
        INC R0              ; Increment pointer for positive storage
        SETB P1.7           ; Set P1.7 high to turn on LED
        SJMP NEXT           ; Jump to NEXT

NEGATIVE:
        MOV @R1, A          ; Store negative number at RAM (90H onwards)
        INC R1              ; Increment pointer for negative storage
        CLR P1.7            ; Clear P1.7 to turn off LED

NEXT:
        DJNZ R2, PROCESS    ; Decrement counter, loop if not zero

HALT:
        SJMP HALT           ; Infinite loop to end execution

END

## add 2 nums 
![alt text](<Screenshot 2025-03-05 at 11.33.55 PM.png>)

##  Status of Program Status Register (PSW) after Addition

After execution:

CY = 0 (No carry out of bit 7)
AC = 1 (Auxiliary carry from bit 3 to 4)
P = 0 (Odd parity)
OV = 0 (No signed overflow)

---
Bit	Symbol	Meaning	Effect After ADD A, #2FH (38H + 2FH = 67H)
7	CY	Carry Flag	0 (No carry from bit 7)
6	AC	Auxiliary Carry	1 (Carry from bit 3 to bit 4)
5	F0	General-Purpose Flag (User-Defined)	Unchanged
4	RS1	Register Bank Select Bit 1	Unchanged (Depends on selected register bank)
3	RS0	Register Bank Select Bit 0	Unchanged (Depends on selected register bank)
2	OV	Overflow Flag (For Signed Numbers)	0 (No overflow)
1	—	Reserved (Unused)	0 (Always 0)
0 	P	Parity Flag (Even parity = 1, Odd parity = 0)	0 (67H has 5 ones → odd parity)
