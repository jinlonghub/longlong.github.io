---
layout: post
title: "Leetcode-8 String to integer (atoi)"
date: 2017-09-23 21:00:00 +0800 
categories: Algorithms
tag: Atoi
---
* content
{:toc}


>[Leetcode 8：String to integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/description/)

---

<!-- more -->

## Description:     
Implement atoi to convert a string to an integer.  

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.  

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.  

Requirements for atoi: 
- The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.  

- The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.  

- If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.  

- If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.   

---
    
<!-- TOC -->

## Solution:    
- 思路：这到题不需要复杂的数据结构，但是需要考虑很多个特殊情况：
      - "___123": 字符串以空格开始，则忽略所有的空格；  
      - "123__4": 空格在中间或者尾部出现，直接返回第一个空格之前的数字；  
      - "+123"/"-123": 如果是"负号"，需要在return的值中显示出来，"正号"在return结果中就不用添加"+"了；  
      - "+-123": 首位置两个符号连续出现，return 0；  
      - "12+-3": 中间或尾部两个符号连续出现，return符号之前的数字；  
      - "ab123": 以非"+" "-" 和数字开始的string，直接return 0；
      - 结果越界时，正数return INT_MAX； 负数return INT_MIN；  

---  

<!-- TOC -->   
       
## C++ Code:     

```cpp

class Solution {
public:
    int myAtoi(string str) {
        long long res = 0;
        int flag = 1;
        bool first = true;
        if (str.length() == 0) return 0;
        for (int i = 0; i < str.length(); i++) {
            if (first && str[i] == ' ') continue;  //去掉前面的空格
            if (!first && str[i] == ' ') break;    //中间和尾部遇到空格，直接break
            if (!isdigit(str[i]) && str[i] != '+' && str[i] != '-') break;  //输入非数字和非+-的情况下，直接break
            if (str[i] == '+' || str[i] == '-') {
                if (first) {  // +- 是第一个有效输入
                    first = false;
                    str[i] == '+' ?  : flag = -1;
                } else {  // +- 不是第一个有效输入
                    return res;
                }  
            }
            if(isdigit(str[i])) {
                res = res * 10 + str[i] - '0';  //result不断的*10往左移位，然后累加
                if (res > INT_MAX) {   //在累加的过程中去判断是否overflow
                    return flag == 1 ? INT_MAX : INT_MIN;
                }
                first = false;
            }
            
        }
        return flag == 1 ? res : -res;      
    }
};

```

---

<!-- TOC -->

## 总结：   
  - 小技巧：
    - 如果是数字的str `str[i] - '0'`可以直接得到数字；同理，如果是字母的str `str[i] - 'a'` `str[i] - 'A'`可以得到当前字母到a(A)的距离。
    - 用标记变量`flag`等，记录数字的正负，或者某一种状态。

---

`2017.09.23`       
