## TASK 1: Generate a sequence of even or odd numbers up to 20.
```
section .bss
  oddnumber resd 1     

section .text
  global _start

_start:
  mov eax, 1        ; we start with 1 because I chose odd number sequence

loop:
  mov [oddnumber], eax ; store current odd number
  add eax, 2        ; adding 2 moves us over the next odd number
  cmp eax, 20       ; checking if we are under the 20 limit
  jle loop    ; if we are, we loop
  mov eax, 1
  int 0x80 

```
## Steps to Run
```
"Running Stepi, I can see EAX increasing and going through the sequence."
layout asm
layout regs
break _start
run
stepi
```
## Task 2 : Find the largest number among the five integer numbers. Use initialize variables, and the output goes to the largest un-initialize variable.
```
section .text
  global _start

_start:
  mov eax, [num1] ; put num1 into eax to begin the tracking of biggest integer
  cmp eax, [num2]    
  jge next1 ; if eax is greater or equal, keep it 
  mov eax, [num2] ; if not greater, update with 2nd number        
step1:
  cmp eax, [num3] ;step1 through 3 will check for greater or equal as well
  jge next2
  mov eax, [num3]
step2:
  cmp eax, [num4]
  jge next3
  mov eax, [num4]
step3:
  cmp eax, [num5]
  jge finish
  mov eax, [num5]
finish:
  mov [largest], eax ;move greatest value for storage and for accessing through gdb
  mov eax, 1 ; exit code
  int 0x80 ; exit code

section .data
  num1 dd 11
  num2 dd 42
  num3 dd 22
  num4 dd 63
  num5 dd 43

section .bss
  largest resd 1

```
## Steps to Run
```
layout asm
layout regs
watch (int) largest
break _start
run
stepi
```
## Results
![image](https://github.com/user-attachments/assets/cc878c4c-e0cf-4988-ac4a-a0bf8eaf68ed)
