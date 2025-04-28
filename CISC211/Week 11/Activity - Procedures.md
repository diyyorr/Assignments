## TASK 1: Generate English uppercase characters from A to Z. After every character, there must be a line feed.
```
section .text
global _start

_start:
    mov eax, 65              ; starting off with ascii for the letter A

alphabet:
    mov [letter], eax            ; putting the ascii of the letter A into eax
    mov ecx, letter
    call output                  ; call procedures for printing and new line
    call linefeed

    inc eax                   ; moving onto the next letter
    cmp eax, 91               ; checking if we went past Z which is 90
    jne alphabet

    call exit                 ; procedure for exit

linefeed:
    mov eax, 10               ; writing newlines
    mov [letter], eax
    mov ecx, letter
    mov eax, 4              
    mov ebx, 1
    mov edx, 1
    int 0x80
    ret

output:
    mov eax, 4                ; writing letters
    mov ebx, 1
    mov edx, 1
    int 0x80
    ret

exit:
    mov eax, 1                
    int 0x80

section .bss
letter resb 1



```
## Steps to Run
```
Assemble the code and run
```
## FlowChart
![image](https://github.com/user-attachments/assets/55596335-7194-4f43-aaa7-58ff8022c399)

