# Task 1 (encryption and decryption)
```
section .data
    message db 'WATER' ; message that I need to encrypt
    secret  db 'PLANT' ; key for message encryption
    hidden  db 0, 0, 0, 0, 0 ; encryption result
    shown   db 0, 0, 0, 0, 0 ; decryption result
    fileName db 'answer.txt', 0 ; file that will hold message and key + results

    line1 db 'Plain text: WATER', 10
    line1_len equ $ - line1

    line2 db 'Key: PLANT', 10
    line2_len equ $ - line2

    line3 db 'Encrypted text: '
    line3_len equ $ - line3

    line4 db 10, 'Decrypted text: '
    line4_len equ $ - line4

section .bss
    file resd 1 ; to direct file and printing functions

section .text
    global _start

_start:
    mov ecx, 0 ; start with ecx at 0 so we can get every character inside original message and key

encrypt:
    cmp ecx, 5 ; 5 characters in great
    jge done_encrypt ; if we go over 5, then we stop because there is no more characters

    mov al, [message + ecx] ; move character from message into memory
    xor al, [secret + ecx] ; do XOR operation with the first character in message and key
    mov [hidden + ecx], al ; save new character into hidden storage

    inc ecx ; continues loop and increases counter to move on to second letter
    jmp encrypt

done_encrypt:
    mov ecx, 0 ; reset counter to 0 for decryption

decrypt:
    cmp ecx, 5
    jge done_decrypt ; move on after hitting all 5 characters

    mov al, [hidden + ecx] ; move character from message into memory 
    xor al, [secret + ecx] ; do XOR operation with the first character in message and key
    mov [shown + ecx], al ; save new character into shown storage 

    inc ecx ; continue loop and increase counter
    jmp decrypt

done_decrypt:
    mov eax, 8 ; syscall to create file
    mov ebx, fileName ; name of the file
    mov ecx, 0666o ; permission flags
    int 0x80
    mov [file], eax ; store the file descriptor

    mov eax, 4
    mov ebx, [file]
    mov ecx, line1 ; write the line with the original message
    mov edx, line1_len
    int 0x80

    mov eax, 4
    mov ecx, line2 ; write the key
    mov edx, line2_len
    int 0x80

    mov eax, 4
    mov ecx, line3 ; text before encrypted message
    mov edx, line3_len
    int 0x80

    mov eax, 4
    mov ecx, hidden ; encrypted mesage
    mov edx, 5
    int 0x80

    mov eax, 4
    mov ecx, line4 ; text before decrypted message
    mov edx, line4_len
    int 0x80

    mov eax, 4
    mov ecx, shown ; decrypted message
    mov edx, 5
    int 0x80

    mov eax, 1 ; exit
    int 0x80

```
# Results
![image](https://github.com/user-attachments/assets/648ddf17-5d03-4760-bf7b-c6ebb62b8275)
![image](https://github.com/user-attachments/assets/371b20fd-d7e1-4b7d-bb64-6a1c9871233f)

# Flowchart and Thought Process
![image](https://github.com/user-attachments/assets/7f1349d6-edf0-4a0e-943f-c0ad81a6b9d4)

# Video
https://github.com/user-attachments/assets/1fb0b6bf-14bb-4a29-9d75-707d205e2509


