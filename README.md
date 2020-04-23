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


























   

 

