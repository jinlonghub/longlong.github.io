---
layout: post
title: "Leetcode-9 palindrome number"
date: 2017-09-23 21:00:00 +0800 
categories: Algorithms
tag: Palindrome
---
* content
{:toc}


>[Leetcode 9：palindrome number](https://leetcode.com/problems/palindrome-number/description/)

---

<!-- more -->

## Description:    

Determine whether an integer is a palindrome. Do this without extra space.  

Some hints:  

Could negative integers be palindromes? (ie, -1)  

If you are thinking of converting the integer to string, note the restriction of using extra space.  

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?  

There is a more generic way of solving this problem.  

---
    
<!-- TOC -->

## Solution:    
- 思路1：将数值的首尾数字拿出来比较，然后把首尾数字都删掉，继续下一次比较。
- 思路2：把原数值翻转，然后比较两个数值是否相同。

---  

<!-- TOC -->   
       
## C++ Code:     

```cpp
//Solution 1：
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        int copy = x;
        int count = 1;
        while (copy >= 10) {
            copy /= 10;
            count *= 10;
        }
        
        while (x != 0 && count != 0) {
            int left = x / count;
            int right = x % 10;
            if (left != right) return false;
            x = (x - left * count) / 10;
            count /= 100;
        }
        return true; 
    }
};


//Solution 2:
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        long long tmp = x, rev = 0;
        while (tmp) {
            rev = rev * 10 + tmp % 10;
            tmp /= 10;
        }
        return rev == x;
};


```

---

<!-- TOC -->

## 总结：   
  - 回文串Palindrome问题和翻转Reverse问题，类似，都需要运用`/`和`%`来处理数字。

---

`2017.09.23`       
