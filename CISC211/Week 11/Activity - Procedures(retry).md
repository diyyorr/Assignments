## TASK 1: Generate English uppercase characters from A to Z. After every character, there must be a line feed.
```
section .text
        global _start

_start:
        mov eax, 65 ; 65 is A in ASCII

print_loop:
        cmp eax, 91 ; 90 = Z so we don't want to go past 90        
        je done ; jump to exit if over 90              
        
        call output ; if not under 90, we call output for the letter and the newline
        call newline           
        
        inc eax ; increase the counter              
        jmp print_loop ; restart process    
        
done:
        call exit              

output:
        mov [letter], eax ; store letter in memory         
        push eax ; save our current letter                        
        mov ecx, letter ; shows system my letter            
        mov edx, 1 ; printing code              
        mov ebx, 1              
        mov eax, 4              
        int 0x80                                 
        pop eax                 
        ret

newline:
        push eax ; save current letter                              
        mov eax, 10 ; 10 stands for new line          
        mov [letter], eax ; put newline into what should print        
        mov ecx, letter  ; printing new line portion          
        mov edx, 1              
        mov ebx, 1              
        mov eax, 4              
        int 0x80                
        pop eax               
        ret

exit:
        mov eax, 1              
        int 0x80                

segment .bss
        letter resb 1              


```
