[TOC]

# size_t和size_type 以及int\ssize_t


size_t是为了方便系统之间的移植而定义的。
在32位系统上定义为 unsigned int
在64位系统上定义为 unsigned long

更准确的说法是在32位系统上是32位无符号整型
在64位系统上是64位无符号整型

 

size_t一般用来表示一种计数，比如有多少东西被拷贝等。
sizeof操作符的结果类型是size_t,
该类型保证能容纳实现所建立的最大对象的字节大小。

它的意义大致是"适于计量内存中可容纳的数据项目的个数的无符号整数类型"。
所以，它在数组下标和内存管理函数之类的地方广泛使用

 

ssize_t:
这个数据类型用来表示可以被执行读写操作的数据块的大小。它和size_t类似，但必须是signed。

再来看下size_t与size_type的区别：

我觉得有一句话总结的很好：
size_t是全局的，而size_type是跟容器相关的。


```
为了使自己的程序有很好的移植性，c++程序员应该尽量使用size_t和size_type而不是int, unsigned。
1. size_t是全局定义的类型；size_type是STL类中定义的类型属性，用以保存任意string和vector类对象的长度
2. string::size_type 制类型一般就是unsigned int, 但是不同机器环境长度可能不同 win32 和win64上长度差别;size_t一般也是unsigned int
3. size_t 使用的时候头文件需要 <cstddef> ；size_type 使用的时候需要<string>或者<vector>
4. 二者联系：在用下标访问元素时，vector使用vector::size_type作为下标类型，而数组下标的正确类型则是size_t。
```
