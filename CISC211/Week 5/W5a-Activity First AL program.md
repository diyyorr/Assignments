## Code for W5A
```SYS_EXIT equ 1
SYS_WRITE equ 4
STDIN equ 0
STDOUT equ 1
section .text
        global _start

_start:
mov eax, SYS_WRITE
mov ebx, STDOUT
mov ecx, msg1
mov edx, len1
int 0x80

mov eax, SYS_WRITE
mov ebx, STDOUT
mov ecx, msg2
mov edx, len2
int 0x80

mov eax, SYS_WRITE
mov ebx, STDOUT
mov ecx, msg3
mov edx, len3
int 0x80

mov eax, SYS_EXIT
mov ebx, 0
int 0x80

section .data
msg1 db 'I came,', 10
len1 equ $ - msg1

msg2 db 'I saw,', 10
len2 equ $ - msg2

msg3 db 'I conquered.', 10
len3 equ $ - msg3
```
## Steps to Run Code
```
; nasm -f elf32 variableredo.asm -o variableredo.o
; ld -m elf_i386 variableredo.o -o variableredo
; ./variableredo
```
