## TASK 1: Write an Assembly code that calculates a factorial of a pre-defined number.
```
section .data
    num dd 5
    newline db 10
    sum db '120', 10
    len equ $ - sum

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, 1 ; start counter
    mov ecx, [num]

loop_start:
    imul eax, ecx ; eax x ecx for first value. will continue to multiply itself by following loop
    dec ecx ; decrease the value as factorial goes -1, -1,
    cmp ecx, 0 
    jne loop_start ; check if 0 if not continue on

    mov [result], eax ; move final result into result section

    mov eax, 4
    mov ebx, 1
    mov ecx, sum ; whole section for printing
    mov edx, len
    int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80


```
## Steps to Run
```
"120 is stored in the result section as well as printed in the terminal with a line break"
layout asm
layout regs
break _start
run
stepi (repeat)
x/d &result

```
## Results
![image](https://github.com/user-attachments/assets/1e9147ca-660b-431f-a3c4-caa99824f7d2)
