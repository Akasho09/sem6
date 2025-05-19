## ✅ 8051 Program: Copy Message from Code ROM to Upper RAM (80H onward) and also to Port 0
```sh
ORG 0000H

MOV DPTR, #400H     ; ROM message starting at 400H
MOV R0, #80H        ; Indirect RAM pointer (upper RAM)
MOV R2, #0AH        ; Assuming message length = 10 bytes

COPY_LOOP:
    CLR A
    MOVC A, @A+DPTR     ; Read from on-chip code ROM
    MOV @R0, A          ; Store to upper RAM using indirect
    MOV P0, A           ; Also output to Port 0 (SFR at 80H)

    INC R0              ; Next RAM address
    INC DPTR            ; Next ROM location
    DJNZ R2, COPY_LOOP  ; Repeat for 10 bytes

END
```

## Write a program in assembly to transfer 50 bytes of data from external data ROM to external data RAM. The external data ROM address starts at 3000H and the external data RAM address starts at 8000H.

```sh 
MOV DPL , 00H ; LOWER DPTR
MOV R0 , 30H ; EXTERNAL ROM ADDRESS HIGHER BITS
MOV R1 , 80H ; EXTERNAL RAM HIGHER BITS 
MOV R3 , 50D ; COUNT 
LOOP : CLR A 
       MOV DPH , R0  ; LOAD DPTR TO 3000 respective to ROM address 
       MOVX A , @DPTR 
       MOV DPH , R1 ; REFRENCE DPTR TO XTERNAL RAM 8000 ONWARDS 
       MOV @DPTR , A ; MOVE DATA 
       INC DPL 
       DJNZ R3 , LOOP
END 
```

## binary to decimal 
```sh
ORG 0000H         ; Program start address

START:
    MOV P2, #0FFH ; Set P2 as input (tri-state high)
    MOV A, P2     ; Read input from P2
    SWAP A        ; Swap nibbles (P2.7-P2.4 → A.3-A.0)
    ANL A, #0FH   ; Now A has value from 0 to 15
    MOV DPTR, #LOOKUP ; Point to lookup table
    MOVC A, @A+DPTR   ; Get decimal equivalent from table
    MOV P1, A         ; Output to P1

    SJMP START        ; Repeat forever

; --- Lookup table (Decimal values for binary 0000 to 1111) ---
LOOKUP:
    DB 00 , 01 , 02 , 03 , ..... , 15   ; decimal equivalent of (00B - 0FB)

END
