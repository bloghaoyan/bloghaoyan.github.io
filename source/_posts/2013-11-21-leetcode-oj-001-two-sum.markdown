---
layout: post
title: "LeetCode OJ 001 Two Sum"
date: 2013-11-21 13:27
comments: true
categories: LeetCode
---

>[Two Sum 两数之和](http://oj.leetcode.com/problems/two-sum/)

###Description:
>Given an array of integers, find two numbers such that they add up to a specific target number.  
>The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.  
>Please note that your returned answers (both index1 and index2) are *not zero-based*.  
>You may assume that each input would have exactly one solution.
<!--more-->
###描述：
>给定一个数组，找出其中两个数加起来等于一个目标数字。  
>函数twoSum返回这两个数的索引值，其中index1小于index2。  
>索引值从1开始而不是0。  
>每个输入有且只有一个解。  

###Input:
>numbers={2, 7, 11, 15}, target=9

###Output:
>index1=1, index2=2

###思路
>1. 暴力法：算法复杂度为O(n<sup>2</sup>)
>2. 先排序，再二分查找：算法复杂度O(nlogn)

###代码
```cpp
class Solution {
public:
    int bSearch(vector<int> &numbers, int other, int low, int high) {
        if (low>high) {
            return -1;
        }
        int mid = (low+high)/2;
        if (other==numbers[mid]) {
            return mid;
        } else if (other>numbers[mid]) {
            bSearch(numbers, other, mid+1, high);
        } else {
            bSearch(numbers, other, low, mid-1);
        }
    }

    vector<int> twoSum(vector<int> &numbers, int target) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        vector<int> backup = numbers;
        sort(numbers.begin(), numbers.end());
        for(int i=0; i<backup.size(); i++) {
            int j = bSearch(numbers, target-backup[i], 0, backup.size()-1);
            if(j!=-1) {
                vector<int> result;
                result.push_back(i+1);
                for(int k=0; k<backup.size(); k++) {
                    if(backup[k]==numbers[j] && k!=i) {
                        result.push_back(k+1);
                    }
                }
                return result;
            }
        }
    }
};
```