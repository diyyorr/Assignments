## TASK 1: Write an Assembly code that calculates a factorial of a pre-defined number.
```
section .data
number dd 5

section .bss
result resd 1

section .text
global _start

_start:

mov eax, [number]
call multiplication
mov [result], eax
call exit

multiplication:
mov ebx, eax
loop:
dec ebx
imul eax, ebx
cmp ebx, 1
jg loop
ret

exit:
mov eax, 1
int 0x80


```
## Results
![image](https://github.com/user-attachments/assets/ecd45f1f-e7d6-4be7-9031-ba52e01030be)
