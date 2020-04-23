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

2. Go to Kali Linux, open a terminal and type
uname-a








   

 

