---
title: CPP随笔
date: 2023-11-03 11:20:31
tags: 随笔
categories: C++
---

## 含非智能指针的类

为含有指针的类的写函数是一个很麻烦的事情，总结了一下经验:
- 注意移动构造函数和移动赋值运算符：需要检查`this!=&that`，防止自我赋值后把自己数据删除的情况。
- 注意复制构造函数和赋值运算符：一般指针存储的是堆上的资源，没有RC的情况下不能直接拷贝。有RC的情况下更麻烦，要检查计数器。
- 所有会用到该类引用/指针的函数（有没有 const 没区别，直接间接引用都算）：同移动构造一样需要检查`this!=&that`，防止函数执行过程中 that 数据改变

虽然只有以上三点，但是实际写起来非常头疼，一不小心就会忘记。~~人生苦短，智能指针能用就用~~ 非性能要求或特殊需求（写驱动等）或者~~折磨~~锻炼自己的情况还是乖乖用智能指针吧。