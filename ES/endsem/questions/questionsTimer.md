## HALF THE SQUARE WAVE IF PERIOD DIRECTLY. 

## Timer-based Square Wave Generation (XTAL = 22 MHz)  . Multiple timers
```yml
ORG 0000H
MAIN:
    MOV TMOD, #01H       ; Timer 0 Mode 1 (16-bit)
    MOV P1, #00H         ; Clear Port 1

LOOP:
    ; 45ms ON
    SETB P1.0
    ACALL DELAY_45MS

    ; 45ms OFF
    CLR P1.0
    ACALL DELAY_45MS

    ; 25ms ON
    SETB P1.0
    ACALL DELAY_25MS

    ; 25ms OFF
    CLR P1.0
    ACALL DELAY_25MS

    ; 4 cycles of 15ms ON/OFF
    MOV R2, #04
REPEAT_15MS:
    SETB P1.0
    ACALL DELAY_15MS

    CLR P1.0
    ACALL DELAY_15MS

    DJNZ R2, REPEAT_15MS

    SJMP LOOP

; Delay Subroutines
DELAY_45MS:
    MOV TH0, #0BDH
    MOV TL0, #08FH
    ACALL TIMER_DELAY
    RET

DELAY_25MS:
    MOV TH0, #04DH
    MOV TL0, #01FH
    ACALL TIMER_DELAY
    RET

DELAY_15MS:
    MOV TH0, #094H
    MOV TL0, #09DH
    ACALL TIMER_DELAY
    RET

TIMER_DELAY:
    CLR TF0
    SETB TR0
WAIT: JNB TF0, WAIT
    CLR TR0
    RET
END

```

-  SETB P1.0 for on-time waveform and CLR P1.0 after that for off-time.
-   MOV R2, #04
and DJNZ R2, REPEAT_15MS
Fot multiple cyckes of same waveform .
- for 45ms we can divide it into 2.
DELAY_45MS:
    MOV R0 , #2
REPEAT :  
    MOV TH0, #0BDH
    MOV TL0, #08FH
    ACALL TIMER_DELAY
    DJNZ REPEAT RO
    RET

## Write a program to count the number of pulses arriving at pin T0 (P3.4) for a time duration of 2 seconds using timer 1. Assume XTAL = 22 MHz. Modify the above code to count for 1 minute.
```sh 
ORG 0000H

START:
    MOV TMOD, #15H       ; Timer 0: Counter Mode 1, Timer 1: Timer Mode 1
    SETB P3.4            ; Configure P3.4 as input for external pulses
    MOV TL0, #00H        ; Clear Timer 0 low byte
    MOV TH0, #00H        ; Clear Timer 0 high byte
    SETB TR0             ; Start Timer 0 (Counter)

    MOV R0, #40          ; Loop 40 times for 2 seconds (40 x 50ms)

DELAY_LOOP:
    MOV TL1, #00H        ; Clear Timer 1 low byte
    MOV TH1, #0B0H       ; Load Timer 1 high byte for 50ms delay
    CLR TF1              ; Clear Timer 1 overflow flag
    SETB TR1             ; Start Timer 1

WAIT: JNB TF1, WAIT        ; Wait until Timer 1 overflows
    CLR TR1              ; Stop Timer 1
    DJNZ R0, DELAY_LOOP  ; Repeat delay loop

    CLR TR0              ; Stop Timer 0 (Counter)

>   MOV A, TL0           ; Move Timer 0 low byte to Accumulator
    MOV P2, A            ; Output low byte to Port 2
    MOV A, TH0           ; Move Timer 0 high byte to Accumulator
    MOV P1, A            ; Output high byte to Port 1

    SJMP START           ; Repeat the process
END
``` 

- input for counter :
    MOV TMOD, #15H       ; Timer 0: Counter Mode 1, Timer 1: Timer Mode 1
>    SETB P3.4            ; Configure P3.4 as input for external pulses
    MOV TL0, #00H        ; Clear Timer 0 low byte
    MOV TH0, #00H        ; Clear Timer 0 high byte
    SETB TR0             ; Start Timer 0 (Counter)

-  output to ports:
    MOV A, TL0           ; Move Timer 0 low byte to Accumulator
    MOV P2, A            ; Output low byte to Port 2
    MOV A, TH0           ; Move Timer 0 high byte to Accumulator
    MOV P1, A            ; Output high byte to Port 1.

### IMPS:
1. TMOD is in Timer1 Mode1 && Counter0 Mode1 or (Timer 0: Counter Mode 1, Timer 1: Timer Mode 1)
2. SETB P3.4      to start counting from pin 3.4 and get results in TH0 and TL0 respective .
3. SETB TR0  to start counter .
4. put 2s timer in between .
5. get no of counts . 

## ✅ Q3: Auto Reload Mode (Mode 2) + 1ms Pulse (XTAL = 11.0592 MHz)
1 Machine Cycle = 1.085 µs
For 1ms delay = ~921 counts ⇒ TL1 = 256 - 921 = -665 → Not possible in 8-bit

### 📘 Explanation: Why Mode 2 is Called Auto-Reload
In Mode 2, the timer is 8-bit and only TLx is incremented.
When it overflows (goes from FFH to 00H), it automatically reloads from THx.
No need to reinitialize the timer in software.
Great for periodic waveforms, baud rate generation, or constant interval interrupts.

-     CPL P3.4            ; Toggle pin P3.4
  after timer , no need to setfirst.

## Use Mode 1 and display the decimal count on P1 and P2 continuously. Set the initial count to 20000.
ORG 0000H
MOV TMOD, #50H        ; Timer 1, Mode 1, external counter
MOV TH1, #04H         ; 4E20H → TH1 = 04H
MOV TL1, #E2H
SETB TR1              ; Start timer
HERE:
    MOV A, TL1
    MOV P2, A
    MOV A, TH1
    MOV P1, A
    SJMP HERE
END


## A 1 Hz external clock signal is fed into pin P3.5 (T1).

- The external 1 Hz signal means we get 1 pulse every second.
```sh 
ORG 0000H

;---------------------------------
; Variable Initialization
;---------------------------------
SEC:     DB 00H     ; seconds
MIN:     DB 00H     ; minutes
HOUR:    DB 00H     ; hours

;---------------------------------
; Main Routine
;---------------------------------
MAIN:
    MOV TMOD , 01100000B ; counter 1 mode 2 
    MOV TL1 , 00H ; we use only TL1 to count secs 
    SETB P3.5 ; set bit for inpuy clock signals 
    SETB TR1 ; set bit for counter 

    ; loop to check for 60s 
LOOP : MOV A , TL0 
       CJNE A, #60 , DISPLAY_TIME 
       ACALL  INC_MINS
       ACALL LOOP

INC_MINS: MOV A , MIN 
          INC A 
          CJNZ A, #60 , INC_HOURS
          MOV MINS , #00
          RET

INC_HOURS: MOV A , HOURS 
           INC A
           MOV HOURS , A
           CJNZ HOURS , #24 , NEW_DAY
           RET

NEW_DAY: MOV HOURS , 00H
         RET


;---------------------------------
; LCD Display Subroutine (Pseudo)
;---------------------------------
DISPLAY_TIME:
    ; You may assume subroutines like DISPLAY_LCD A exist
    ; Display HH:MM:SS
    MOV A, HOUR
    ACALL DISPLAY_LCD

    MOV A, #':'
    ACALL DISPLAY_LCD

    MOV A, MIN
    ACALL DISPLAY_LCD

    MOV A, #':'
    ACALL DISPLAY_LCD

    MOV A, SEC
    ACALL DISPLAY_LCD

    RET

;---------------------------------
; End of Program
;---------------------------------
END


