# Assign three integers to the variables x, y, and z and pass on the function name of your choice. The function task is to add three variables and assign the result to the 'result' variable. 

```
section .data ; creating the variables for x,y,z
        x dd 10
        y dd 11
        z dd 12

section .bss
        result resd 1 ; creating the result storage


section .text
        global _start

_start:

        push dword [x] ; push the numbers inside the variables into the stack
        push dword [y]
        push dword [z]

        call adding ; call the function that I created to add the numbers

        mov [result], eax ; after the function is done, I place the number into result so I can see it in gdb

        mov eax, 1 ; exit code
        int 0x80

adding:

        push ebp ; preserve ebp
        mov ebp, esp ; point ebp to the current stack

        mov eax,[ebp+8] ; move z or 12 into eax
        add eax,[ebp+12] ; add y or 11 to eax
        add eax,[ebp+16] ; add x or 10 to eax

        leave ; clean up allocated memory when function finishes
        ret
```
# Steps to Run
```
gdb ./quiz4
break _start
run
stepi (12 times)
x/d &result (check result variable)
```
# Result 
![image](https://github.com/user-attachments/assets/65880e8d-7420-4ef5-a7a4-e4a88b13232d)
