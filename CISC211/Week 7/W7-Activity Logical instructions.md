## Code for Part 1 of Activity Logical Instructions
```
section .text
global _start

_start:
mov eax, 7
xor eax, eax

mov ebx, eax ; moving the result "0" into ebx gives us the exit status 0 which stands for success
mov eax, 1
int 0x80      
```
## Steps to Run 
```
nasm -f elf32 xor.asm -o xor.o
ld -m elf_i386 xor.o -o xor
./xor
echo $?      
```
## Code for Part 2 of Activity Logical Instructions
```
section .text
global _start

_start:
mov eax, 8
test eax, 1
jz even                 
                                
mov eax, 1             
mov ebx, 1 ;if not even, gives 1 exit status meaning odd
int 0x80

even:
mov eax, 1     
mov ebx, 0 ;if even, gives 0 exit status meaning even
int 0x80

```
## Steps to Run 
```
nasm -f elf32 -o test.o test.asm
ld -m elf_i386 -o test test.o
./test
echo $?  
```
