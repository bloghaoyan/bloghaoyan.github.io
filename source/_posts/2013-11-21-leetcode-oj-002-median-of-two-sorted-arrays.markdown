---
layout: post
title: "LeetCode OJ 002 Median of Two Sorted Arrays"
date: 2013-11-21 20:59
comments: true
categories: LeetCode
---
>[Median of Two Sorted Arrays 两个已排序数组的中值](http://oj.leetcode.com/problems/median-of-two-sorted-arrays/)

###Description:
>There are two sorted arrays A and B of size m and n respectively.   
>Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
<!--more-->
###描述：
>给定两个已排序的数组A和B，大小分别为m和n。  
>找出这两个数组的中值。  
>要求时间复杂度为O(log (m+n))。  

###思路
>相当于做归并。本题中若m+n为偶数则中值是中间两个数的平均值。

###代码
```cpp Median of Two Sorted Arrays
class Solution {
public:
    double findMedianSortedArrays(int A[], int m, int B[], int n) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        int mid = (m+n)/2;
        int *temp = new int[mid+1];
        int i = 0;
        int j = 0;
        int k = 0;
        for(; i<m && j<n && k<=mid; k++) {
        	if(A[i]<B[j]) {
        		temp[k] = A[i++];
        	} else {
        		temp[k] = B[j++];
        	}
        }

        if(i==m) {
        	for(; k<=mid; k++) {
        		temp[k] = B[j++];
        	}
        } else if(j==n) {
        	for(; k<=mid; k++) {
        		temp[k] = A[i++];
        	}
        }
        double result = 0;
        if((m+n)%2 == 0) {
        	result = (temp[mid]+temp[mid-1])/2.0;
        } else {
        	result = temp[mid]*1.0;
        }

        delete[] temp;
        return result;
    }
};
```