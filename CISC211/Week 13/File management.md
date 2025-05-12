# Create a text-based file called "quotes.txt" and add the following contents. Append the following quotes in the same file. 
```
section .data
    filename db "quotes.txt", 0 ; creating file name

    quote1 db "To be, or not to be, that is the question.", 10, 10 ; all 4 quotes being defined to write to the file
    len1 equ $ - quote1

    quote2 db "A fool thinks himself to be wise, but a wise man knows himself to be a fool.", 10, 10
    len2 equ $ - quote2

    quote3 db "Better three hours too soon than a minute too late.", 10, 10
    len3 equ $ - quote3

    quote4 db "No legacy is so rich as honesty.", 10, 10
    len4 equ $ - quote4

section .bss
    fd resb 1 ; for file descriptor

section .text
    global _start

_start:
    mov eax, 8 ; using sys_creat to create the file
    mov ebx, filename
    mov ecx, 0711o
    int 0x80
    mov [fd], eax

    mov eax, 4 ; writing the first quote to file
    mov ebx, [fd]
    mov ecx, quote1
    mov edx, len1
    int 0x80

    mov eax, 4 ; second quote to file
    mov ebx, [fd]
    mov ecx, quote2
    mov edx, len2
    int 0x80

    mov eax, 6 ; using sys_close to close the file
    mov ebx, [fd]
    int 0x80

    mov eax, 5 ; using sys_open to re open the file
    mov ebx, filename
    mov ecx, 2 ; opening in read/write mode
    mov edx, 0711o
    int 0x80
    mov [fd], eax

    mov eax, 19 ; moving file descriptor to the end so it does not overwrite                        
    mov ebx, [fd]                      
    mov ecx, 0                         
    mov edx, 2                         
    int 0x80

    mov eax, 4 ; writing 3rd quote ot the file
    mov ebx, [fd]
    mov ecx, quote3
    mov edx, len3
    int 0x80

    mov eax, 4 ; writing 4th quote to the file
    mov ebx, [fd]
    mov ecx, quote4
    mov edx, len4
    int 0x80

    mov eax, 6 ; closing file
    mov ebx, [fd]
    int 0x80

    mov eax, 1 ; exit program
    int 0x80

```
# Steps to Run
```
Aseemble the Code
./file
cat words.txt
```
# Result 
![image](https://github.com/user-attachments/assets/f31c44df-523e-424b-ade2-b6a5b08cdbf7)

# Challegenes
```
My hardest challenge was realizing that after writing and closing the file, reopening it resets the file pointer to the beginning.
I expected it to keep writing at the end, because the file descriptor was there but it didn’t. I had to use sys_lseek to move the file descriptor to the end before writing again, otherwise it would overwrite the original quotes.
```
