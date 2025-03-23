## Code for Week 6 Arithmetic Assignment 
```
section .data
var1 dd 10      
var2 dd 5       
var3 dd 7
var4 dd 8      

section .bss
result1 resd 1
result2 resd 1
result3 resd 1
result4 resd 1      

section .text
global _start

_start:
;Equation 1: result= -var1*10
mov eax, [var1]
neg eax
imul eax, 10
mov [result1], eax    

;Equation 2: result= var1+var2+var3+var4
mov eax, [var1]
add eax, [var2]
add eax, [var3]
add eax, [var4]
mov [result2], eax    

;Equation 3: result= (-var1*var2)+var3
mov eax, [var1]
neg eax
imul eax, [var2]
add eax, [var3]
mov [result3], eax    

;Equation 4: result= (var1*2)/(var2 - 3) 
mov eax, [var1]
imul eax, 2
mov ebx, [var2]
sub ebx, 3
xor edx, edx
div ebx
mov [result4], eax
        

mov eax, 1
xor ebx, ebx
int 0x80

```
## Steps to Run Code 
```
nasm -f elf32 arithmetic.asm -o arithmetic.o
ld -m elf_i386 arithmetic.o -o arithmetic
./arithmetic
```
