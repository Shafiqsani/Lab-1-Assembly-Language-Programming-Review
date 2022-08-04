
# Lab 1: Assembly Language Programming Review

Lab Instructions
 *   This lab activity comprises two parts, namely Lab tasks, and Post-Lab Viva session. 
 *   Each group to upload completed lab report on LMS for grading.
 *   The students will start lab task and demonstrate each lab task separately for step-wise evaluation
 *   There are related questions in this activity give complete answers. Also provide complete code and results

**Objective:** The aim of this lab is to revise / learn Assembly Language instructions.

**Lab Task 1:**
 
 Define three arrays to hold five one-byte integers each. Initialize the first two with the numbers: 2,3,4,5,6,  and 3,4,5,6,7.Use  nested loop to multiply  corresponding  elements  of  arrays using addition. Display the resultant array using dumpmem and use Push and POP to save loop count (Note:  2*3=2+2+2, )

#### CODE:
```
INCLUDE Irvine32.inc
.data
array1 BYTE 2,3,4,5,6
array2 BYTE 3,4,5,6,7
array3 BYTE 5 DUP(0)
.code
main PROC
mov ecx, lengthof array1
mov ebx, OFFSET array2
mov esi, OFFSET array1
mov edi, OFFSET array3
L1:
push ecx
mov ecx, [ebx]
mov eax, 0
L2:
add eax, [esi]
loop L2
mov [edi], eax
inc edi
inc esi
inc ebx
pop ecx
loop L1
mov esi,OFFSET array3
mov ecx,LENGTHOF array3
mov ebx,TYPE array3
call DumpMem
exit
main ENDP
END main

```
**Lab Task 2:**
 
 Write and execute Assembly code for following program.
Take integer from user and calculate its factorial if input integer is between 3 and 5 output error statement and exit.(Note: Make use of  conditional jumps)

#### CODE:
```
TITLE Factorial calculator
INCLUDE Irvine32.inc
.data
msg1 byte "Enter the number of which factorial found: ", 0
msg2 byte "Factorial: ", 0
msg3 byte "Number is not between 3 and 5", 0
.code
main PROC
mov edx, offset msg1 ; moving offset of msg1 for printing
call writestring ;Print msg1 string
call  Readint ; taking input from user
cmp eax, 3
jnl L2
L2:
cmp eax, 5
jg L3

factorial:
mov ecx, eax ;moving user input to ecx as counter
mov eax, 0001h ; initialize eax with 1
L1:
  mul ecx
  loop L1
mov edx, offset msg2 ; moving offset of msg2 for printing
call writestring ; Print string
call writedec ;Print factorial
exit

L3:
mov edx, offset msg3 ; moving offset of msg2 for printing
call writestring ; Print string
exit
main ENDP
END main


```
**Lab Task 3:**
 
Write and execute assembly code to get 32 bit Hex number from user using ReadHex and find number one’s in 32 bit hex number using bit wise operations and display your count.

#### CODE:
```
INCLUDE Irvine32.inc
.data
msg1 byte "Enter a 32-bit hexadecimal number: ", 0
msg2 byte "Number of ones in 32-bit hex number: ", 0

.code
main proc
mov edx, offset msg1
call writestring ;Print msg1 string
call readhex     ; taking hexadecimal input from user

mov cx, 32;      ; loop for 32-bit binary number
mov ebx,0;

L1:
   shr eax,1     ; shift right the binary number 1 bit
   jnc zero      ; jump if bit is zero
   inc bl        ; increment if the bit is 1
zero: loop L1

mov edx, offset msg2
call writestring
mov eax,ebx
call writedec
main endp

END main


```
