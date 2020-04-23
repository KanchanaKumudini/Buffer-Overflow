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



   

 
