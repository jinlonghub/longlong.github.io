---
layout: post
title: "Leetcode-42 Trapping rain water"
date: 2017-09-22 21:00:00 +0800 
categories: Algorithms
tag: Prefix Sum
---
* content
{:toc}


>[Leetcode 42：Trapping rain water](https://leetcode.com/problems/trapping-rain-water/description/)

---

<!-- more -->

## Description:    
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai).   
n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0).   
Find two lines, which together with x-axis forms a container, such that the container contains the most water.  

Note: You may not slant the container and n is at least 2.   

  ### Example:     
Given [1,3,2], the max area of the container is 2.

---
    
<!-- TOC -->

## Solution:    
- 思路：
  - 要计算总的蓄水量，先求出到每个节点的`max_height`，用`max_height - cur_height`，得到这一个立柱上的蓄水量，然后所有立柱求sum。  
  - 在计算`max_height`时，使用**Prefix_sum思路**，先从左往右求出`cur`左边的`left_max`，再从右往左求出`cur`右边的`right_max`，然后从`left_max`和`right_max`找到min，即`max_height`。  

---  

<!-- TOC -->   
       
## C++ Code:     

```cpp

class Solution {
public:
    int trap(vector<int>& height) {
        if (height.empty()) return 0;
        
        vector<int> left_max(height.size(), 0);
        vector<int> right_max(height.size(), 0);
        int left = 0;
        int right = 0;
        int res = 0;
        
        for (int i = 0; i < height.size(); i++) {
            left = max(left, height[i]);
            left_max[i] = left;
        }
        
        for (int j = height.size() - 1; j >= 0; j--) {
            right = max(right, height[j]);
            right_max[j] = right;  
            //注意：为了确保下标和left的一致性，这里不能写成right_max.push_back(right)。
        }
        
        for (int n = 0; n < height.size(); n++) {
            res += min(left_max[n], right_max[n]) - height[n];
        }
        return res;
    }
};

```

---

<!-- TOC -->

## 总结：   
  - 利用prefix sum的思路求解，将整体的问题，转化为零散结果的加和。

---

`2017.09.22`       
