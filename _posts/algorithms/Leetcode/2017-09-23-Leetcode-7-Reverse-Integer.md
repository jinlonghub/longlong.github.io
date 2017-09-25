---
layout: post
title: "Leetcode-7 Reverse Integer"
date: 2017-09-23 21:00:00 +0800 
categories: Algorithms
tag: Reverse
---
* content
{:toc}


>[Leetcode 7：Reverse Integer](https://leetcode.com/problems/reverse-integer/description/)   

---

<!-- more -->

## Description:     
Reverse digits of an integer.    

Example1: x = 123, return 321   
Example2: x = -123, return -321    

Note:    
The input is assumed to be a 32-bit signed integer. Your function should return 0 when the reversed integer overflows.     
---
    
<!-- TOC -->

## Solution:    
- 思路：利用`/`和`%`完成数字的反转。

---  

<!-- TOC -->   
       
## C++ Code:     

```cpp

class Solution {
public:
    int reverse(int x) {
        long long res = 0;  //这里用long long型存储返回值，为了避免溢出，详见下面**总结**
        int copy = x;
        while (copy != 0) {
            res = res * 10 + copy % 10;
            copy /= 10;
        }
        if (res > INT_MAX) return 0;
        if (res < INT_MIN) return 0;
        return res;
    }
};

```

---

<!-- TOC -->

## 总结：   
  - 使用`/`和`%`小技巧，来完成数字反转、一维小标转换二维下标的问题。    
  - long long int：在C11版本中，加入了`long long int`类型。`long long int`是64位的，即    
    signed long long `-2^31 ~ 2^31 - 1`    
    unsigned long long `0 ~ 2^63 - 1`    
    注：int 和 long型，都是32 bit存储，只有long long型才是64 bit存储。  
  - 强制转换规则：  
    - long long型强制转换为int，会丢失一部分高位数值，但是转换后的int型数字，**不会变为负数**    
    - 如果是int型，如果发生溢出问题，原本的正数则可能变为负数，所以这道题用long long 存储返回值。  

---

`2017.09.23`       
