---
layout: post
title: "Leetcode-42 Trapping rain water"
date: 2017-09-22 21:00:00 +0800 
categories: Algorithms
tag: Two Pointers
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
  - Two Pointers，指向数组的首/尾，两个指针做比较找到min，用`min * 两个指针的距离`表示volume，设置一个全局变量max，volume和max做比较保留最大值，最后return max。
  - 两个指针的移动规则：移动min指针，因为当前volume是min决定的，所以只有移动这个决定因素，才能找到更大的volume，否则如果移动较大的指针，则其volume还是由min决定。
  - Talk is cheap, so let me show the code.

---  

<!-- TOC -->   
       
## C++ Code:     

```cpp

class Solution {
public:
    /*
     * @param heights: a vector of integers
     * @return: an integer
     */
    int maxArea(vector<int> &heights) {
        // write your code here
        if (heights.empty()) return 0;
        
        int left = 0, right = heights.size() - 1;
        int max_vol = 0;
        
        while (left <= right){
            if (heights[left] < heights[right]) {
                max_vol = max(max_vol, heights[left] * (right - left));
                left++;
            } else {  
              /*这里可以把>=合起来考虑，也可以添加一个else if 把=单独拎出来让left++; right--;这都是可以的。
              相比较，单独考虑=时循环次数会少一些。
              
              else if (heights[left] == heights[right]) {
                  max_vol = max(max_vol, heights[left] * (right - left));
                  left++;
                  right--;
              }
              */
                max_vol = max(max_vol, heights[right] * (right - left));
                right--;
            }
        }
        return max_vol;
    }
};

```

---

<!-- TOC -->

## 总结：   
  - Two Pointers的问题有两个注意点：
    - 1. 在进行while循环时的判断条件，是用`<`还是`<=`这个需要根据不同情况慎重考虑。
    - 2. 两个指针的移动规则，这个解题的关键，只有设置正确的移动规则，才能正确解决问题。这个暂时没有总结出规律，只能具体情况具体分析。

---

`2017.09.22`       
