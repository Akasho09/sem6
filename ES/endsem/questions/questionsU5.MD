## 1. Why do we put an LJMP instruction at address 0?
Address 0 is the reset vector in the 8051 microcontroller. When the microcontroller is powered on or reset, it starts executing from memory location 0x0000.

LJMP (Long Jump) is typically placed at address 0 to redirect execution to the actual start of the main program, which may be located at a different memory address (e.g., 0x0100 or beyond) to avoid conflict with interrupt vectors.

🧠 Why LJMP?
LJMP allows jumping anywhere in the 64 KB code space.
Prevents overlap between initialization code and interrupt vectors (addresses like 0x0003, 0x000B, etc.).

🔧 Example:
```yml
ORG 0000H
LJMP MAIN ; Jump to the main program

ORG 0100H
MAIN:
  ; Actual code begins here
```

## ✅ 2. Differentiate Between RET and RETI Instructions

| Feature            | `RET`                             | `RETI`                                            |
| ------------------ | --------------------------------- | ------------------------------------------------- |
| Meaning            | Return from subroutine            | Return from Interrupt                             |
| Usage              | Used at the end of a function     | Used at the end of an ISR                         |
| Functionality      | Pops PC from stack                | Pops PC from stack + informs interrupt controller |
| Interrupt Handling | No effect on interrupt controller | Tells interrupt controller that ISR is finished   |

- Why We Cannot Use RET Instead of RETI at the End of an ISR?
RETI not only returns from the interrupt like RET, but it also notifies the interrupt controller that the ISR has ended and the system is ready for the next interrupt.

If we use RET instead of RETI, the program may return properly, but:

The interrupt controller is not notified, leading to interrupts not being re-enabled or malfunction in nested interrupts.

🚫 Consequences of using RET in ISR:
Interrupt controller state may remain incorrect.

Future interrupts may be ignored.

System behavior may become unpredictable.

- Both perform the same actions of popping off the top two bytes of the
stack into the program counter, and marking the 8051 return to where
it left off.
However, RETI also performs an additional task of clearing the
interrupt-in-service flag, indicating that the servicing of the interrupt
is over and the 8051 now can accept a new interrupt on that pin. If
you use RET instead of RETI as the last instruction of the interrupt
service routine, you simply block any new interrupt on that pin after
the first interrupt, since the pin status would indicate that the interrupt
is still being serviced. In the cases of TF0, TF1, TCON.1, and
TCON.3, they are cleared due to the execution of RETI.

## Light the LED connected to pin 3.0 if the switch connected to pin P3.2 is pressed and light the LED connected to pin 3.1 if the switch connected to pin P3.3 is pressed.

1. Generate a square wave of 2 KHz at P1.2 using timer 1 in mode 1 (XTAL = 22 MHz)
```sh
ORG 0000H
LJMP MAIN

ORG 001BH             ; Timer1 ISR address
TIMER1_ISR:
    CPL P1.2          ; Toggle pin to generate square wave
    MOV TH1, #0FFH
    MOV TL1, #078H
    RETI

ORG 0030H
MAIN : 
MOV TMOD, #10H        ; Timer 1, mode 1
MOV TH1, #0FFH        ; Load high byte
MOV TL1, #078H        ; Load low byte
SETB TR1              ; Start Timer 1
SETB EA               ; Enable global interrupts
SETB ET1              ; Enable Timer1 interrupt

```


2. Recieve data serially and send to p2.



## Write a program to generate a square wave if 50Hz frequency on pin P1.2. This is similar to Example 9-12 except that it uses an interrupt for timer 0. Assume that XTAL=11.0592 MHz

ORG 0
LJMP MAIN

ORG 000BH ; ISR for Timer 0
CPL P1.2
MOV TL0,#00
MOV TH0,#0DCH
RETI

ORG 30H
;--------main program for initialization
MAIN: MOV TM0D,#00000001B ;Timer 0, Mode 1
MOV TL0,#00
MOV TH0,#0DCH
MOV IE, #82H ; enable Timer 0 interrupt
SETB TR0
HERE: SJMP HERE
END

- define ISR at its respective location ie CPL P1.2 and load values into TH1 , TL1 .
-   Main program sets initial values , `enables` Timer in IE register and SETB TR0 to `start` timer .