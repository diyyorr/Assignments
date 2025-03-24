## Calculate the mean of the following dataset using assembly language
```
section .text
global _start

_start:


mov eax, [student1]
add eax, [student2]
add eax, [student3]
add eax, [student4]
add eax, [student5]
mov ebx, 5
xor edx, edx
div ebx

mov ebx, eax
mov eax,1
int 0x80

section .data
student1 dd 60
student2 dd 70
student3 dd 90
student4 dd 40
student5 dd 65

```
## Steps to Run Code 
```
nasm -f elf32 mean.asm -o mean.o
ld -m elf_i386 mean.o -o mean
gdb ./mean
break _start
run
stepi ;9 times
info registers ;to see the final value which is 65
```
## Convert 575 decimal into binary and hexadecimal
```
575/2 = 287 r 1
287/2 = 143 r 1
143/2 = 71 r 1
71/2 = 35 r 1
35/2 = 17 r 1
17/2 = 8 r 1
8/2 = 4 r 0
4/2 = 2 r 0
2/2 = 1 r 0
1/2 = 0 r 1
Binary : 1000111111
/////////////////////
575/16 = 35 r 15 = F
35/16 = 2  r 3  = 3
2/16 = 0  r 2  = 2
Hex = 0x23F
```
## Convert 0x80 into binary
```
0x80 = 128

128/2 = 64 r 0
64/2 = 32 r 0
32/2 = 16 r 0
16/2 = 8 r 0
8/2 = 4 r 0
4/2 = 2 r 0
2/2 = 1 r 0
1/2 = 0 r 1
Binary = 10000000
```
## Convert -10 into binary using 1's and 2's complements
```
10 = 00001010
Flipped 10 = 00001010 → 11110101
```
## Identify error(s) in the following code
```
section .text
    global _start

_start:
    mov eax,10
    mov ebx,20
    add eax,ebx
    mov result,eax
    
    mov eax,1
    int 0x80

section .data
    result resb 1

; Use section .bss for result and mov [result], eax that way you are moving your result into the actual storage and not label
```
## Transfer the bits into the Cache memory
```

```
