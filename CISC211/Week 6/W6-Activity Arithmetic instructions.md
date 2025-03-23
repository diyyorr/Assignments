## Code for Week 6 Arithmetic Assignment 
```
section .data
a dd 10      ; a=10
b dd 5       ; b=5
c dd 2       ; c=2

section .bss
result resd 1    

section .text
global _start

_start:
; Equation 1: a + b
mov eax, [a]
add eax, [b]
mov [result], eax    ; result = a + b

; Equation 2: a - b
mov eax, [a]
sub eax, [b]
mov [result], eax    ; result = a - b

; Equation 3: a * c
mov eax, [a]
imul eax, [c]
mov [result], eax    ; result = a * c

; Equation 4: a / c
mov eax, [a]
mov ebx, [c]
xor edx, edx         
div ebx
mov [result], eax    ; result = a / c (integer division)

mov eax, 1
xor ebx, ebx
int 0x80

```
