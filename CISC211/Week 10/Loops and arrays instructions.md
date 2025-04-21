## TASK 1: Generate a counter using an EBX register
```
section .text
        global _start

_start:
        mov ebx, 0 ; start counter at 0

loop:
        inc ebx ; increases by 1
        cmp ebx,10  ; checking here to make sure its under 10
        jl loop ; if still under 10, then we do the loop again

        mov eax, 1
        int 0x80

```
## Steps to Run
```
"Running Stepi, I can see EBX increasing after going through the loop steps so it is acting as a counter for the amount of times it loops"
layout asm
layout regs
break _start
run
stepi (repeat)
info registers (repeat)
```

## TASK 2: Calculate the final number of the first 10 Fibonacci numbers starting from 0
```
section .text
        global _start

_start:
        mov eax, 10 ; telling system that we will run through 10 numbers
        mov ebx, 0 ; ebx will hold all of the numbers added up
        mov ecx, fib ; first number in array put into ecx to add with ebx later on

loop:
        add ebx, [ecx] ; adding
        add ecx, 4 ; skipping to next number
        dec eax ; decrease our loop counter
        jnz loop ; does not equal to zero then we loop again

        mov eax, 1
        int 0x80

section .data
        fib dd 0, 1, 1, 2, 3, 5, 8, 13, 21, 34

```
## Steps to Run
```
"Stepi until the program reached the exit code. I receive 55 in my ebx registers which confirms the counting/adding was successful"
layout asm
layout regs
break _start
run
stepi (repeat)
```
## TASK 3: Define the array with length 4 and, type integer, find the largest element in the array.
```
section .text
        global _start

_start:
      mov eax, [array] ; first number placed into eax to be compared
      mov ecx, array
      add ecx, 4 ; move to 2nd number
      mov edx, 3 ; 3 numbers left in loop

loop:
      cmp eax, [ecx] ; comparing
      jge next ; greater than or equal, then move on
      mov eax, [ecx] ; if not, update eax with new bigger number

next:
    add ecx, 4 ; move to next number in array
    dec edx ; substract one from the loop counter
    jnz loop ; if loop counter is not 0, then loop again

    mov eax, 1
    int 0x80

section .data
  array dd 15,16,17,18

```
## Steps to Run
```
"Ran Stepi until the exit code and was left with 18 in my eax register confirming that it works"
layout asm
layout regs
break _start
run
stepi (repeat)
```

## Flow Chart and Challenges
![image](https://github.com/user-attachments/assets/e3cede8a-230a-46e3-86d4-33afe9d0f166)

