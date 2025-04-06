## Suppose that the sensor is connected to port P1 that reads the temperature readings after some interval. Write a program in assembly that:

Stores 15 temperature readings at RAM locations 40H onwards.

If the temperature reading is positive, save it at RAM locations 60H onwards.

If the temperature reading is negative, save it at RAM locations starting from 90H.

Also, if the temperature is positive, send a high bit to the LED connected to pin P0.7, else send a low bit at 87H.

--- 

ORG 0000H        ; Origin at address 0000H
MOV R0, #40H     ; Initialize R0 to point to RAM location 40H for storing readings
MOV R1, #60H     ; Initialize R1 to point to RAM location 60H for positive readings
MOV R2, #90H     ; Initialize R2 to point to RAM location 90H for negative readings
MOV R3, #15      ; Counter for 15 readings

READ_LOOP:
    ACALL DELAY  ; Call delay subroutine to wait for the next reading
    MOV A, P1    ; Read temperature value from port P1
    MOV @R0, A   ; Store the reading at current R0 address
    INC R0       ; Increment R0 to point to the next storage location

    ; Check if the temperature reading is positive or negative
    JB ACC.7, NEGATIVE   ; If MSB (bit 7) of ACC is 1, it's negative; jump to NEGATIVE

POSITIVE:
    MOV @R1, A   ; Store positive reading at current R1 address
    INC R1       ; Increment R1 for next positive reading storage
    SETB P0.7    ; Set P0.7 to turn on LED for positive reading
    SJMP CONTINUE

NEGATIVE:
    MOV @R2, A   ; Store negative reading at current R2 address
    INC R2       ; Increment R2 for next negative reading storage
    CLR P0.7     ; Clear P0.7 to turn off LED for negative reading

CONTINUE:
    DJNZ R3, READ_LOOP  ; Decrement R3; if not zero, repeat loop

END


## 
ORG 0000H        ; Set origin at address 0000H
MOV DPTR, #200H  ; Initialize DPTR to point to ROM address 200H
MOV R4, #00H     ; Initialize count register R4 to 0
MOV R5, #100     ; Initialize loop counter R5 to 100

READ_LOOP:
    CLR A                ; Clear accumulator
    MOVC A, @A+DPTR      ; Load data byte from ROM into accumulator
    MOV B, A             ; Move data byte to register B for comparison

    ; Compare with lower limit R2
    MOV A, B             ; Move data byte back to accumulator
    CLR C                ; Clear carry flag
    SUBB A, R2           ; A = A - R2
    JC NEXT_BYTE         ; If carry set, data < R2, skip increment

    ; Compare with upper limit R3
    MOV A, R3            ; Load upper limit into accumulator
    CLR C                ; Clear carry flag
    SUBB A, B            ; A = R3 - data
    JC NEXT_BYTE         ; If carry set, data > R3, skip increment

    ; Data is within range [R2, R3]
    INC R4               ; Increment count

NEXT_BYTE:
    INC DPTR             ; Move to next data byte in ROM
    DJNZ R5, READ_LOOP   ; Decrement loop counter; if not zero, repeat loop

    ; Output the count to port P2
    MOV A, R4            ; Move count to accumulator
    MOV P2, A            ; Send count to port P2

END


## Check if String in ROM (300H onwards) is Palindrome
```java
ORG 0000H

; Step 1: Initialize DPTR to point to ROM address 300H
MOV DPTR, #0300H      ; DPTR points to beginning of string
MOV R0, #00H          ; R0 will count length of the string

; Step 2: Find the length of the null-terminated string
FIND_LEN:
    MOV A, @DPTR      ; Get character from code memory
    INC DPTR          ; Move to next character
    INC R0            ; Increment length counter
    CJNE A, #00H, FIND_LEN ; Keep going until null character (00H)
    DEC R0            ; Adjust length by -1 to ignore null terminator

; Step 3: Initialize pointers for palindrome check
MOV R1, #00H          ; R1 = Start index (left)
MOV R2, R0            ; R2 = End index (right)
DEC R2                ; R2 = R0 - 1

; Step 4: Compare characters from both ends
PAL_CHECK:
    ; Load character from left (R1)
    MOV DPTR, #0300H  ; Base address
    MOV A, R1
    MOVC A, @A+DPTR   ; A = code[300H + R1]
    MOV B, A          ; Save in B for comparison later

    ; Load character from right (R2)
    MOV A, R2
    MOVC A, @A+DPTR   ; A = code[300H + R2]
    CJNE A, B, NOT_PAL ; If not equal, jump to NOT_PAL

    ; Increment left index, Decrement right index
    INC R1
    DEC R2
    CJNE R1, R2, PAL_CHECK ; Repeat until pointers meet

; Step 5: If all matched, output 'Y' to P1
PAL:
    MOV A, #'Y'       ; ASCII 'Y'
    MOV P1, A         ; Output Y to port P1
    SJMP DONE

; Step 6: If mismatch found, output 'N' to P1
NOT_PAL:
    MOV A, #'N'       ; ASCII 'N'
    MOV P1, A         ; Output N to port P1

; Step 7: End
DONE:
    SJMP $            ; Infinite loop

END

```
