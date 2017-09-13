---
layout: post
title: "Leetcode-146 LRU Cache"
date: 2017-09-12 21:00:00 +0800 
categories: Algorithms
tag: Hash
---

<!-- more -->

---
## [LRU Cache](https://leetcode.com/problems/lru-cache/description/)
---

### Description:    
>Design and implement a data structure for Least Recently Used (LRU) cache.     
>It should support the following operations: **get** and **put**.    
>**get(key)** - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.    
>**put(key, value)** - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.     


### Follow up:    
>Could you do both operations in O(1) time complexity?    

### Example:     
>LRUCache cache = new LRUCache( 2 /* capacity */ );    
>    
>cache.put(1, 1);    
>cache.put(2, 2);    
>cache.get(1);       // returns 1    
>cache.put(3, 3);    // evicts key 2    
>cache.get(2);       // returns -1 (not found)    
>cache.put(4, 4);    // evicts key 1    
>cache.get(1);       // returns -1 (not found)    
>cache.get(3);       // returns 3    
>cache.get(4);       // returns 4    

---
    
### Solution:    
- 首先明确LRU是如何工作的：    
1. LRU的容量是3，先将|1|2|3|放进去1是队尾 3是队首，现在4出现，则需要把队尾的1删掉，把4加到队首。--> 对应操作：**从尾部删除，从头部加入**    
2. LRU现在为|2|3|4|，现在3出现，需要把3删掉，再把3加到队首，即|2|4|3|。-->对应操作:**从中间删除，从头部加入**     
       
- 选择数据结构：    
-- 满足上面操作的，可以有queue、heap、LinkedList，基于O(1) 的时间复杂度，所以先去LinkedList，因为queue和heap无法在O(1)时间内删除中间元素。        
-- 但是LinkedList不支持从中间删除元素的操作，我们再搭配一个Hash map，map的_key_记录在List中的位置，_value_记录ListNode。    
>Java函数库中自带LinkedHashMap。    
>- LinkedList 需要区分single(_单向链表_) 和 double(_双向链表_)：（_这两个的区别主要是在对delete的处理上_）    
>- single list：因为ListNode中只能存放next的节点，所以，使用single list的时候，HashMap中_value_就不要存放当前的_node_，而是存_node->pre_ 。这样在delete操作时就不用再去寻找_node->pre_。         
>- double list：相比single list，双向链表要方便一些，所以这里采用双向链表。      

---     
       
### C++ Code:     

```cpp
class ListNodes {
public:
    int val;
    ListNodes *pre, *next;
    ListNodes(int v, ListNodes *p, ListNodes *n) {
        val = v;
        pre = p;
        next = n;
    }
};

class LRUCache{
public:
    int capac, size;
    unordered_map<int, ListNodes *> hashmap;
    unordered_map<ListNodes *, int> hashmap2;
    //这里的hashmap2是为了在capacity占满情况下，删除最后一个元素用的， 
    //因为无法知道tail->pre在hashmap中的key，所以使用hashmap2来帮助寻找。
    ListNodes *head, *tail;
    
    // @param capacity, an integer
    LRUCache(int capacity) {
        // write your code here
        capac = capacity;
        head = new ListNodes(0, NULL, NULL);
        tail = new ListNodes(0, head, NULL);
        head->next = tail;
        size = 0;
        hashmap.clear();
        hashmap2.clear();
    }
    
    // @return an integer
    int get(int key) {
        // write your code here
        int res = -1;
        if (hashmap.find(key) != hashmap.end()) {
            res = hashmap[key]->val;
            //delete key in LinkedList
            auto node = hashmap[key];
            ListNodes *pre = node->pre, *next = node->next;
            pre->next = next;
            next->pre = pre;
            //put key to the head of List
            node->pre = head;
            node->next = head->next;
            head->next->pre = node;
            head->next = node;
        }
        return res;
    }

    // @param key, an integer
    // @param value, an integer
    // @return nothing
    void put(int key, int value) {
        // write your code here
        if (hashmap.find(key) != hashmap.end()) {
            //delete key in LinkedList
            auto node = hashmap[key];
            node->val = value;  
            //注上一行：key在hashmap中找到后，需要更新hashmap的value，
            //因为找到的node马上就要删除，所以其value要更新为新put进来的value。
            ListNodes *pre = node->pre, *next = node->next;
            pre->next = next;
            next->pre = pre;
            //put key to the head of List
            node->pre = head;
            node->next = head->next;
            head->next->pre = node;
            head->next = node;
        } else {
            if (size == capac) {
                ListNodes *n = tail->pre;
                n->pre->next = tail;
                n->next->pre = n->pre;
                size--;
                int k = hashmap2[n];
                hashmap.erase(k);
                hashmap2.erase(n);
            }
            //put key to the head of List
            ListNodes *n = new ListNodes(value, head, head->next);
            head->next->pre = n;
            head->next = n;
            hashmap.insert(make_pair(key, n));
            hashmap2.insert(make_pair(n, key));
            size++;
        }
    }
};

```

---

### 总结：   
- 这是一个hash 和 链表结合的题目，考查的非常高频。重点练习。     
- Java中有专门的函数库： LinkedHashMap = DoublyLinkedList + HashMap     

---

`2017.09.12` SHANGHAI     
