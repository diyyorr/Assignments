## 1. Write an x86-compatible assembly code
```
; result = (var1 + 2) / (var3 - var2) = (7 + 2) / (9 - 8) = 9 / 1 = 9

section .data
var1 dd 7
var2 dd 8
var3 dd 9

section .bss
result resb 1

section .text
global _start

_start :

mov eax, [var1] ; (var1 + 2)
add eax, 2

mov ebx, [var3] ; (var3 - var2)
sub ebx, [var2]

xor edx, edx ; (var1 + 2) / (var3 - var2)
div ebx

add eax, '0' ; turn 9 into ascii for printing
mov [result], al
mov eax, 4
mov ebx, 1
mov ecx, result ; printing portion of the code
mov edx, 1
int 0x80

mov eax, 1
int 0x80
```
## Steps to Run
```
nasm -f elf32 exem.asm -o exem.o
ld -m elf_i386 exem.o -o exem
./exem ; will get 9 returned to terminal
gdb ./exem
break _start
run
si
si
si
si
info registers ; will see EAX register with 0x9 and EDX with 0
```
## Results
```
Register Name : Eax = 9 (Quotient) after division
Register Name : Edx = 0 (Remainder) after division
```
![image](https://github.com/user-attachments/assets/d3684e2e-20d6-4fc0-90a6-6ced74813501)

![image](https://github.com/user-attachments/assets/a495dd96-fcec-4171-a0ba-7c394481d34b)


## 2. Using a K-map, simplify the following equation. 


## Write a code that identifies an odd or an even number
```
section .data
  number dd 14   ; variable which is used for test                   
  even_msg db "even number" ; created the message and len for the test
  even_len equ $ - even_msg
  odd_msg db "odd number"
  odd_len equ $ - odd_msg

section .text
  global _start

_start:
  mov eax, [number]              
  mov ebx, 2                      
  xor edx, edx    ; divide the variable by two. remainder is stored in edx because eax is the quotient                
  div ebx                         

  test edx, edx     ; testing to see if edx == 0                 
  jz even                  

odd:
  mov eax, 4
  mov ebx, 1
  mov ecx, odd_msg ;created two labels for two different outcomes. odd prints odd message. even does even.
  mov edx, odd_len
  int 0x80
  mov eax, 1 
  int 0x80

even:
  mov eax, 4
  mov ebx, 1
  mov ecx, even_msg ; code for when remainder is 0
  mov edx, even_len
  int 0x80
  mov eax, 1 
  int 0x80 
```
## Steps to Run
```
nasm -f elf32 oddeven.asm -o oddeven.o
ld -m elf_i386 oddeven.o -o oddeven
./oddeven
```
## Results
![image](https://github.com/user-attachments/assets/f8ad6f1d-b626-4a53-af60-392c2f5fcd15)
