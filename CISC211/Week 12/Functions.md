## TASK 1: Assign a number to a register or a variable, pass a number to the function and display the result, 'odd' or 'even'.
```
section .data
    even_msg db "even", 10 ; instructions for printing even
    even_len equ $ - even_msg

    odd_msg db "odd", 10 ; isntructions for printing odd
    odd_len equ $ - odd_msg

section .text
    global _start

_start:
    push 58642 ; inputting the number I want to check
    call evenorodd ; then calling our function to check it

    mov eax, 1
    xor ebx, ebx ; exit code
    int 0x80

evenorodd:
    push ebp ; preserving my ebp
    mov ebp, esp ; new base pointer

    mov eax, [ebp+8] ; get 58642
    and eax, 1 ; check lowest bit (0 is even, 1 is odd)
    cmp eax, 0
    je even ; if even then go to even function if not, then it goes to odd function

odd:
    mov eax, 4
    mov ebx, 1
    mov ecx, odd_msg ; printing for odd
    mov edx, odd_len
    int 0x80
    jmp end

even:
    mov eax, 4
    mov ebx, 1
    mov ecx, even_msg ; printing for even
    mov edx, even_len
    int 0x80

end:
    leave
    ret
```
## Steps to Run
```
Assemble Code
Run Code
See Result
```
## Result & Flowchart
