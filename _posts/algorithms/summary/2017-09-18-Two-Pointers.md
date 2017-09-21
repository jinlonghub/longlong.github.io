---
layout: post
title: "Array专题--Two Pointers"
date: 2017-09-18 17:00:00 +0800 
categories: Algorithms
tag: Array
---
* content
{:toc}

---

<!-- more -->

## Array专题--Two Pointers    

---

## Two Pointers解题思路              
  - 比如遇到Two sum这类问题，有两种解题思路：  
    - HashMap方法：(题意：给定一个数组，从中找到两个元素的**下标**，其相加和target相等)    
      - 建立hashmap，存储当前元素的`值`和`下标`；        
      - 用target减去每一个当前元素，得到的值 在hashmap中查找，如果有这个`值`则返回其`下标`，也返回当前的`下标`。    

    - Sort + Two Pointers方法：  (题意：给定一个数组，从中找到两个**元素**(注意这时是**元素**不是**下标**了)，其相加和target相等)    
      - 首先，把数组排序`sort()`，时间复杂度为`O(n logn)`       
      - 然后，生成两个指针`left`和`right`指向首元素和尾元素，移动两个指针去和target做比较。这个pair的过程 时间复杂度`O(n)`  
      - 整体时间复杂度：`O(n logn) + O(n)`     

---

## Two Pointers相关题目      

### 1. [Leetcode Link：Two Sum](https://leetcode.com/problems/two-sum/description/)      

  + **Description**          
    Given an array of integers, return indices of the two numbers such that they add up to a specific target.    
    You may assume that each input would have exactly one solution, and you may not use the same element twice.      

  + **Example**           
    Given nums = [2, 7, 11, 15], target = 9, Because nums[0] + nums[1] = 2 + 7 = 9, return [0, 1].    

  + **Solution**      
    - 使用Hashmap的方法：建立hashmap，存储当前元素的`值`和`index`；        
    - 用target减去每一个当前元素，得到的值 在hashmap中查找，如果有这个`值`则返回其`index`，也返回当前的`index`。   

  + **C++** **Code**              

```cpp  

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> hashmap;
        vector<int> result;
        if (nums.size() == 0) return result;
        
        for (int i = 0; i < nums.size(); i++) {
            
            if (hashmap.find(target - nums[i]) != hashmap.end()) {
                result.push_back(hashmap[target - nums[i]]);
                result.push_back(i);
            }
            hashmap.insert(make_pair(nums[i], i));
        }
        return result; 
    }
};


```

---

### 2. Two Sum Closest （无连接）   

  + **Description**  
    Given an array of integers, return the difference of the sum of two numbers such that it is the closest to a specific target.      
    You may assume that each input would have exactly one solution, and you may not use the same element twice.   

  + **Example**  
    Given nums = [-1, 2, 1, -4], target = 4, the closest difference is 1.   

  + **Solution**   
    - Sort + Two Pointers方法，根据题意有一个变形，需要设置一个全局的diff，来存储最接近target的差值。

  + **C++** **Code**              

```cpp  

class Solution {
public:
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    int twoSumClosest(vector<int>& nums, int target) {
        // Write your code here
        sort(nums.begin(), nums.end());
        int n = nums.size();
        int j = n - 1;
        int diff = INT_MAX;
        for (int i = 0; i < n; ++i) {
            while (i < j && nums[i] + nums[j] > target) {
                if (nums[i] + nums[j] - target < diff)
                    diff = nums[i] + nums[j] - target;
                j --;
            }
            
            if (i >= j) break;

            if (target - nums[i] - nums[j] < diff)
                diff = target - nums[i] - nums[j];
        }
        return diff;
    }
};


```

---

### 3. [Leetcode Link：Three Sum](https://leetcode.com/problems/3sum/description/)       

  + **Description**   
    Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.  
    Note: The solution set must not contain duplicate triplets.  

  + **Example**  
    given array S = [-1, 0, 1, 2, -1, -4],     
    A solution set is: { [-1, 0, 1], [-1, -1, 2] }   

  + **Solution**   
    - 大体思路：先把3_Sum的问题，简化为2_Sum，然后再按 Sort + Two Pointers方法，去解决2_Sum。需要注意，在求3_Sum的过程中要去重。 
    - 具体操作：将原数组sort排序，从左到右for一遍所有元素，依次元素cur，把cur后面的元素当做一个数组，寻找出2_Sum = target - cur的。
    - 代码执行中去重的操作：比如  
      >array S = [-1, 0, 1, 2, -1, -4]，其中有两个`-1`，每次取一个值后都和它之前的取值做比较，相同的就跳过。
    - 时间复杂度：for一遍数组需要O(n)时间，每次for取到一个cur后又在遍历cur之后的元素，这是O(n-1~n) 简化为O(n)，所以整体是O(N^2)的时间复杂度。  
    - 在这里可以对比一下，hashmap和Sort+Two Pointer 的区别：
      - 假设用hashmap解决这个问题，需要建立两个hashmap去存储cur的`值`与`index`和`target - cur`后的2_Sum中某个元素的`值`与`index`，时间复杂度为O(n^2)，但空间复杂度却是需要多耗费O(n)的空间。
      - 相比之下，Sort + Two Pointers方法优于hashmap，因为其时间复杂度也是O(n^2)，但是没有耗费额外的空间。
     
  + **C++** **Code**              

```cpp  
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        if (nums.size() == 0) return res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 2; i++) {
            if (nums[i] > 0) break;  //sort之后从小到大排列，当前取的三个值中最小的都`>0`则直接break。
            //如果不break，会出现超时的错误。
            if (i > 0 && nums[i - 1] == nums[i]) continue;  //去重
            int left = i + 1, right = nums.size() - 1;
            while(left < right) {
                if (nums[left] + nums[right] < (0 - nums[i])) {
                    left++;
                } else if (nums[left] + nums[right] > (0 - nums[i])) {
                    right--;
                } else {
                    res.push_back({nums[i], nums[left], nums[right]});
                    while(left < right && nums[left + 1] == nums[left]) left++;  //去重
                    while(left < right && nums[right - 1] == nums[right]) right--;  //去重
                    left++;
                    right--;
                }
            }
        }
        return res;
    }
};

    
```

<!-- TOC -->

## 总结：   
Two pointer在解决Two_Sum和3_Sum、4_Sim问题(返回的是元素本身)时，虽然时间复杂度不低，但这是目前找到的最优解了，后面有更好的解法再更新。

---

`2017.09.18`       
