---
layout: post
title: "Array专题--Partition Array"
date: 2017-09-21 13:00:00 +0800 
categories: Algorithms
tag: Array
---
* content
{:toc}

---

<!-- more -->

## Array专题--Partition Array   

---

## Partition Array解题思路              
  - 也是使用Two Pointers的基本方法，加上了二分的思想：用两个指针去同时遍历数组时，将比较的结果去做二分处理。
  - Partition有二分和三分的题型，二分："Partition Array"；三分："Sort Colors"

---

## Partition Array相关题目      

### 1. [Lintcode Link：Partition Array](http://www.lintcode.com/en/problem/partition-array/)      

  + **Description**          
    Given an array nums of integers and an int `k`, partition the array (i.e move the elements in "nums") such that:  
    >All elements < k are moved to the left  
    >All elements >= k are moved to the right  
    Return the partitioning index, i.e the first index i nums[i] >= k.     

    Notice:  
    You should do really partition in array nums instead of just counting the numbers of integers smaller than k.
    If all elements in nums are smaller than k, then return nums.length 

  + **Example**           
    If nums = [3,2,2,1] and k=2, a valid answer is 1.    

  + **Solution**      
    - 使用Two Pointer方法，使用`left` `right`表示数组首、尾下标，寻找`nums[left] >= k`的值，和`nums[right] < k`的值；然后swap `nums[left]和nums[right]`  
    - 注意最后`return`的是`right + 1`

  + **C++** **Code**              

```cpp  

class Solution {
public:
    int partitionArray(vector<int> &nums, int k) {
        if (nums.empty()) return -1;
        int left = 0, right = nums.size() - 1;
        while (left <= right) {
            while (left <= right && nums[left] < k) left++;
            while (left <= right && nums[right] >= k) right--;
            if (left <= right) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
        return right + 1;
    }
};

```

---

### 2. [Leetcode Link：Sort Colors](https://leetcode.com/problems/sort-colors/description/)   

  + **Description**  
    Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.  
    Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.   

    Note:  
    You are not suppose to use the library's sort function for this problem.   
    click to show follow up.    

  + **Example**    
    Given [1, 0, 1, 2], sort it in-place to [0, 1, 1, 2].   

  + **Solution** 
    - 使用三分的思想，将`[0, 1, 2]` 分到三个部分。  




---

<!-- TOC -->

## 总结：   


---

`2017.09.18`       
