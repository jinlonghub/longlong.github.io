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
    - 注意最后`return`的是`right + 1`：见下面代码，在最终退出while循环时right指向的是最后一个`<k`的值，所以第一个`>=k`的值就需要`right + 1`。  

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
    - 使用三分的思想，建立三个指针，一个首指针一个尾指针，另一个遍历数组，遍历中0的元素放到首指针左边，2的元素放到尾指针右边，1的元素本地不动。这样就把数组分为了`[0,1,2]`的顺序。    
    - 具体操作：建立三个指针`left`指向数组首， `right`指向数组尾， `i` 初始值为0 遍历数组；用`i`去遍历数组，`nums[i] == 0`时`nums[i]`和`nums[left]`交换，`nums[i] == 2`时`nums[i]`和`nums[right]`交换，`nums[i] == 1`时不做操作 继续遍历下一个元素。  

  + **C++** **Code**              

```cpp  

class Solution {
public:
    /*
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    void sortColors(vector<int> &nums) {
        // write your code here
        int left = 0, right = nums.size() - 1;
        int i = 0;
        
        while (i <= right) {  
          //这个判断条件非常关键，是i和right做比较，不是left和right比较！！！
          //因为left,i,right分别代表了0,1,2的区域，当i和right相遇即1和2的分界已经找到，可以退出循环了。
          //如果i，right相遇后还继续走，就会把之前已经排好的顺序打乱。
          //为什么必须用 <= ，因为right指向的点是没有做过判断的，只有i和right重叠，才能保证i对所有点做了比较。
            if (nums[i] == 0) 
                int tmp = nums[i];
                nums[i] = nums[left];
                nums[left] = tmp;
                left++;
                i++;  
                //因为i是从左往右遍历，所以从left交换过来的只能是0或1，所以和left交换后i可以直接++。
                //这里i++节省了循环的次数
                //如果不i++,则会出现malloc错误：
                //Main: malloc.c:3722: _int_malloc: Assertion `(unsigned long) (size) >= (unsigned long) (nb)' failed. Aborted (core dumped) 
            } else if (nums[i] == 1) {
                i++;
            } else {
                int tmp = nums[i];
                nums[i] = nums[right];
                nums[right] = tmp;
                right--;
            }
        }
    }
};


```  

---

<!-- TOC -->

## 总结：  
  - Partition Array基本使用的是Two Pointers的思考方式，在设置while循环的退出条件时，需要慎重考虑，大多数情况下使用`<=`这种带着等号的判断基本不会出错，但具体情况需要具体分析。


---

`2017.09.18`       
