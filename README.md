# Buffer-Overflow Writeup
Stack Based Buffer Overflow 
This writeup is based on the Stack Buffer Overflow Video


Introduction

Copying source buffer into destination buffer could result in overflow when source string length is greater than destination string length.
There are two types of buffer overflow:
1. Stack Based Buffer Overflow - In this the destination buffer resides in stack
2. Heap Based Buffer Overflow - In this the destination buffer resides in heap

What is a Stack?

A stack is an abstract data type frequently used in computer science. A stack of objects has the property that the last object placed on the stack will be the first object removed. This property is commonly referred to as last in, first out queue, or a LIFO.
Several operations are defined on stacks. Two of the most important are PUSH and POP. PUSH adds an element at the top of the stack. POP, in contrast, reduces the stack size by one by removing the last element at the top of the stack.

![1](https://user-images.githubusercontent.com/50174329/80055208-c226a300-853e-11ea-889e-1c0ec3be2ab9.PNG)

What is Stack Buffer Overflow?

In software, a stack buffer overflow or stack buffer overrun occurs when a program writes to a memory address on the program's call stack outside of the intended data structure, which is usually a fixed-length buffer. Stack buffer overflow bugs are caused when a program writes more data to a buffer located on the stack than what is actually allocated for that buffer. This almost always results in corruption of adjacent data on the stack, and in cases where the overflow was triggered by mistake, will often cause the program to crash or operate incorrectly. Stack buffer overflow is a type of the more general programming malfunction known as buffer overflow (or buffer overrun). Overfilling a buffer on the stack is more likely to derail program execution than overfilling a buffer on the heap because the stack contains the return addresses for all active function calls.

Let's do a Slack Based Buffer Overflow

1. First disable memory randomization and enable core dumps.

![2](https://user-images.githubusercontent.com/50174329/80057143-88a46680-8543-11ea-9d8e-b77f44e96906.PNG)

2. Go to Kali Linux, open a terminal and type: uname -a you can see that I'm using Kali linux 2016 32 bits version.

![3](https://user-images.githubusercontent.com/50174329/80057850-411eda00-8545-11ea-9b0a-bd8b9021c8c1.PNG)

3. Turn off memory address randomisation.

![4](https://user-images.githubusercontent.com/50174329/80058085-f2257480-8545-11ea-9a96-e925a3c8655a.PNG)

4. Reload that and run the memory address randomisation command again to get the value 0.

![5](https://user-images.githubusercontent.com/50174329/80058943-3f0a4a80-8548-11ea-8ad9-4dc215965c35.PNG)

5. Enable debugging and core dump to unlimited.

![6](https://user-images.githubusercontent.com/50174329/80059110-bd66ec80-8548-11ea-8140-4e2d08ddbefa.PNG)

6. Type prinenv and press enter to show all the variables running around the infrastructure and close that out.

![7](https://user-images.githubusercontent.com/50174329/80059370-788f8580-8549-11ea-9e0b-a43e12eb20a5.PNG)

7. Type nano, paste the script, press Ctrl o and call it exvexec.sh and press Ctrl x to exit.

![12](https://user-images.githubusercontent.com/50174329/80060898-54ce3e80-854d-11ea-83ff-672ce367c97f.PNG)

![8](https://user-images.githubusercontent.com/50174329/80059572-f489cd80-8549-11ea-8530-ea3d44586ecc.PNG)

8. Type nano and chmod +x exvexec.sh to execute this and you will see the executable in green.

![9](https://user-images.githubusercontent.com/50174329/80059872-b9d46500-854a-11ea-8a4d-72c2885a8bd4.PNG)

9. Type nano, paste vuln code, press Ctrl o and call it vuln.c and press Ctrl x to exit, type nano and chmod + x vuln.c to execute this and you will see the executable in green. 

![13](https://user-images.githubusercontent.com/50174329/80061052-bc848980-854d-11ea-8e40-a3275d1d9917.PNG)

![10](https://user-images.githubusercontent.com/50174329/80060168-81815680-854b-11ea-89e3-e548e5970ee3.PNG)

by default the C program shows the int main fuctio, int argc is the count of arguments, char argv is the character array of values and next line we created a character buffer of 500 bites and we run the very vulnerable function string copy. This says that the argv value [1] and copy that into buffer. The problem is that if argv value is more than 500 it will overflow the buffer. Then type Ctrl x to exit.

10. Type nano, ls, and we can see our exvexec.sh and our vuln.c program. 

![11](https://user-images.githubusercontent.com/50174329/80060787-091b9500-854d-11ea-98f0-64f41953c154.PNG)

11. Compile this using the guines compiler to create an executable file.

![14](https://user-images.githubusercontent.com/50174329/80061214-446a9380-854e-11ea-970b-5b9d5ec92d82.PNG)

12. Type ls and ./envexec.sh -d vuln to clean up the bash environment. 

![15](https://user-images.githubusercontent.com/50174329/80061387-bfcc4500-854e-11ea-9c15-0d4a02794e3f.PNG)

13. Now we are inside GDB.

![16](https://user-images.githubusercontent.com/50174329/80061501-19cd0a80-854f-11ea-9a1f-59096e0ad2bc.PNG)

14. Run some GDB Commands.

![17](https://user-images.githubusercontent.com/50174329/80061690-9d86f700-854f-11ea-9f2b-f9a60b3b4e3e.PNG)

15. Type disas main to Disassemble main, you will find an interesting assembly code defining the buffer and go ahead and hex convert it.

![18](https://user-images.githubusercontent.com/50174329/80061960-3289f000-8550-11ea-8f12-6bdfd7afe7b4.PNG)

![19](https://user-images.githubusercontent.com/50174329/80061972-3b7ac180-8550-11ea-8f84-f32a8ffd397f.PNG)

16. Run Hello to run the vuln program and exit it normally.

![20](https://user-images.githubusercontent.com/50174329/80062182-c1970800-8550-11ea-9ab2-4f739ebae921.PNG)

17. Next run $(python -c 'print "\x41" * 508') to over run the program and the program will receive a signal with segmentation fault and we have crashed the program.

![21](https://user-images.githubusercontent.com/50174329/80062499-8c3eea00-8551-11ea-92cf-5bc283cf1386.PNG)

![22](https://user-images.githubusercontent.com/50174329/80062511-91039e00-8551-11ea-8e78-87671d779491.PNG)

18. Type info refisters and you will see that the eip (Extended Index Pointer) and ebp (Extended Base Pointer) have been over written with the values 4141.

![23](https://user-images.githubusercontent.com/50174329/80062941-73830400-8552-11ea-84f2-c848b9ac661d.PNG)

19. Type x/200x ($esp - 550) to examine the memory address and run that command to walk trough the memory.

![24](https://user-images.githubusercontent.com/50174329/80063176-f1dfa600-8552-11ea-8fc8-114e448bf69c.PNG)

![25](https://user-images.githubusercontent.com/50174329/80063183-f60bc380-8552-11ea-8539-942128c3643e.PNG)

20. Now we can see where the buffer exists in memory and where it has been over written.

![26](https://user-images.githubusercontent.com/50174329/80063334-5569d380-8553-11ea-8ddf-59849229da11.PNG)

21. To over write the value 41 with 51 run the command run $(python -c 'print "\x90" * 426 + "\x31\xc0\x83\xec\x01\x88\x04\x24\x68\x2f\x7a\x73\x68\x2f\x62\x69\x6e\x68\x2f\x75\x73\x72\x89\xe6\x50\x56\xb0\x0b\x89\xf3\x89\xe1\x31\xd2\xcd\x80\xb0\x01\x31\xdb\xcd\x80" + "\x51\x51\x51\x51" * 10')

![27](https://user-images.githubusercontent.com/50174329/80063613-e6d94580-8553-11ea-838c-c7c404079277.PNG)

type y and this time the return vale is 51 instead of 41 that means we were able to successfully over right the return address and the caller EBP.

22. Again type info registers and we can see that the eip and ebp has been over written.

![28](https://user-images.githubusercontent.com/50174329/80063930-9d3d2a80-8554-11ea-9f32-45ae2ce2fa28.PNG)

23. Next type x/200x ($esp - 550) to double check memory and press enter.

![29](https://user-images.githubusercontent.com/50174329/80064214-2a807f00-8555-11ea-8907-0bbec007ec9d.PNG)

24. Pick a value.

























































   

 

