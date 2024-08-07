---
layout: default
title: java 21 notes
nav_order: 1 
parent: java
grand_parent: Computer Language
---

## Java 21 Notes

### switch

### sealed

### var

### 


### 2.2 The Basics
. complied language

    source -> compile -> object
    source -> compile -> object -> link -> executable

. minimal C++

    int main(){}

    #include<iostream>   //include iostream

    std::cout << "Hello world"  //  << put to


ADDITION::
https://www.geeksforgeeks.org/c-c-include-directive-with-examples/

** include directive

Syntax:

. #include "user-defined_file"

    Including using ” “: When using the double quotes(” “), the preprocessor access the current directory in which the source “header_file” is located. This type is mainly used to access any header files of the user’s program or user-defined files.

. #include <header_file>

    Including using <>: While importing file using angular brackets(<>), the the preprocessor uses a predetermined directory path to access the file. It is mainly used to access system header files located in the standard system directories.

### 2.2.2 Types,Variables, and Arithmetic

    sizeof(char)  //1
    sizeof(int)   //4

    double d1 = 2.3
    complex<double> z2 = {1,2}

   . auto

     auto b = true

### 2.2.3 Constants
. const    //evaluate at runtime
. constexpr  // evaluate at compile time

### 2.2.4 Test and Loops

### 2.2.5 Pointers, Arrays and Loops

. Array

   char v[6];

. Pointer

   char* p;   //pointer to character

A pointer variable can hold the address of an object of the appropriate type.

char* p = &v[3];

char x = *p

prefix unary * means "contents of"
prefix unary & means "address of"

### 2.3 User-Defined Types

### Understanding pointers

1.  “指针”通常用于保存一个地址，这个地址的数据类型在定义指针变量时确定。

For example:
```c++
int a; //定义一个变量a，用于保存一个int类型。
int* b; //定义一个指针变量b，用于保存一个地址，这个地址所保存的数据应该是int类型。
```

2.  一般不会给指针直接赋值一个数值，而是将其他变量的地址赋值给指针，或者其他指针的值赋值给这个指针。
3.  
```cpp
   b=&a; //把变量a的地址赋值给b。“&”操作是取变量的地址。
```
   
   ```cpp
   int* c; //我们又定义一个指针c
   c=b; //将b的值赋值给c，
   ```
   
   上面已经知道b是指针，它的值是a的地址，那么现在c 的值和b一样，也是个a的地址。
   
1.  指针变量保存的值，也就是地址是可以变的。
```cpp
int d[100];
int* e;
e=&d[0]; //e保存了数组d的第一个数据的地址
for (int i=0; i<100; i++){
    *e = 0; //把该地址中的数据赋值0
    e++; //地址累加一次，也就是数组中下一个数据的地址
    }
```
指针和其他变量一样，可以运算（一般是加减），也可以重新赋值。

1. 指针的用途。

   比方说，我们有个函数，如下：
   ```cpp
   int add（int x){
    return (x+1);//把输入的值加1并返回结果
   } 
   ```
   
   应用的时候是这样的：
   ```cpp
   { int a=1;
     a = add(a);
   } //add函数返回的是a+1//现在 a等于2
   ```
   就是把a都累加一次
   
   用指针怎么写：
```cpp
   void add(int *y){ //给入的是一个int指针，是一个地址。
   *y = *y + 1; //* 是指引用 这个地址所保存的变量
   }
   //这条语句的意思就是，把这个地址里的值加1，然后放回这个地址
   ```
   把这个函数用起来：
```cpp
   {
    int a=1;
    add(&a);
   } //把a的地址传到函数里//add函数，就是把a的值加1，再放回到变量a里。//现在a等于2}
   ```
   
   对一个数据结构里的数据进行处理，就可以传入这个结构的地址，在函数中依靠指针来引用这个地址的数据结构，进行运算。
   
5. 若已有一个指针变量，可不可以用另外一个指针来保存这个变量的地址呢。可以的。一个变量保存另一个指针的地址，那它就是通常所说是“指针的指针”了。通常，指针的指针多用做（或指的是）函数指针或数据结构中有指针的情况.
   
   
6. 一个变量要赋值后才能用，指针也是一样。一般把指针赋值为Null，就是表明这个指针是空的，不能用。所以程序中一定要经常判别指针不是Null才能用。
7. 
8. 把复合的语句拆开来看，比较容易理解。
   ```cpp
   int* a = &b;  
   ```
这种，拆成
   ```cpp
   int* a;
   a=&b;  
   ```
就好理解了.