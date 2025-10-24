# MPMC_SKILL-ASSESSMENT1
## AIM
To write and execute an 8086 assembly language program to search for a given number in an array of N elements and display whether the number is FOUND or NOT FOUND.
---

## APPARATUS REQUIRED
- 8086 Microprocessor Kit or Emulator, Assembler (TASM/MASM), 8086 Simulator Software (e.g., EMU8086), and a Computer System.

---

## ALGORITHM

1. Start the program.


2. Initialize the Data Segment using MOV AX, DATA and MOV DS, AX.


3. Load the starting address of the array into register SI.


4. Load the number of elements (N) into register CL.


5. Load the search element into register AL.


6. Set a flag register (e.g., BL = 0) to indicate “not found.”


7. Compare the search element (AL) with each element of the array:

If a match is found, set BL = 1 and jump to step 9.

Otherwise, increment SI to point to the next element and decrement CL.



8. Repeat step 7 until all elements are checked (CL = 0).


9. If BL = 1, display “NUMBER FOUND”, else display “NUMBER NOT FOUND.”


10. Terminate the program using interrupt INT 21H (function 4CH).
  

---

## FLOWCHART
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/6478bf0f-1dcf-44a9-a384-424199e488b9" />


---

## PROGRAM
```
DATA SEGMENT
    ARR DB 10, 20, 30, 40, 50     ; Array of 5 elements
    N   DB 5                      ; Number of elements
    NUM DB 30                     ; Number to search
    MSG1 DB 'NUMBER FOUND$'
    MSG2 DB 'NUMBER NOT FOUND$'
DATA ENDS

CODE SEGMENT
ASSUME CS:CODE, DS:DATA

START:
    MOV AX, DATA
    MOV DS, AX

    MOV CL, N            ; Load number of elements
    LEA SI, ARR          ; Load address of array
    MOV AL, NUM          ; Load number to search

NEXT:
    CMP AL, [SI]         ; Compare with array element
    JE FOUND             ; If equal, jump to FOUND
    INC SI               ; Move to next element
    DEC CL               ; Decrease count
    JNZ NEXT             ; If not zero, continue loop

NOTFOUND:
    LEA DX, MSG2         ; Load "NOT FOUND" message
    MOV AH, 09H
    INT 21H
    JMP EXIT

FOUND:
    LEA DX, MSG1         ; Load "FOUND" message
    MOV AH, 09H
    INT 21H

EXIT:
    MOV AH, 4CH
    INT 21H

CODE ENDS
END START


```
## OUTPUT

<img width="640" height="480" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/a6bf05af-072a-4585-8e66-c481a51336ba" />



---


## RESULT

The program was successfully executed and verified using the 8086 simulator.

When the number is present in the array, the output displayed:
“NUMBER FOUND”

When the number is not present, the output displayed:
“NUMBER NOT FOUND”
