---
layout: post
title: "LeetCode OJ 005 Longest Palidromic Substring"
date: 2013-11-23 20:35
comments: true
categories: LeetCode
---
>[Longest Palindromic Substring 最长回文子串](http://oj.leetcode.com/problems/longest-palindromic-substring/)

###Description:
>Given a string S, find the longest palindromic substring in S.   
>You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

###描述：
>给定一个字符串S，找出S中的最长回文子串。  
>你可以假设字符串的最大长度为1000，其中有且只有一个最长回文子串。

###思路
>Manacher算法

###代码
```cpp
class Solution {
public:
	string longestPalindrome(string s) {
		// IMPORTANT: Please reset any member data you declared, as
		// the same Solution instance will be reused for each test case.
		int longSize = s.size() * 2 + 2;
		string sLong = string(longSize, '#');
		sLong[0] = '$';
		for (int i = 0; i < s.size(); i++) {
			sLong[i * 2 + 2] = s[i];
		}
		int *radi = new int[longSize];
		for (int i = 0; i < longSize; i++) {
			radi[i] = 0;
		}

		int high = 0;
		int i = 0;
		int cur = 0;

		for (i = 1; i < longSize; i++) {
			if (high > i) {
				radi[i] = min(radi[2 * cur - i], high - i);
			} else {
				radi[i] = 1;
			}
			while (sLong[i - radi[i]] == sLong[i + radi[i]]) {
				radi[i]++;
			}
			if (i + radi[i] > high) {
				cur = i;
				high = i + radi[i];
			}
		}

		int max = 1;
		int pos = 1;
		for (int i = 1; i < longSize; i++) {
			if (radi[i] > max) {
				max = radi[i];
				pos = i;
			}
		}

		int start = 0;
		int subLen = 0;
		if (pos % 2 == 0) {
			pos = (pos - 2) / 2;
			max = max / 2;
			subLen = max * 2 - 1;
		} else {
			pos = (pos - 3) / 2;
			max = (max - 1) / 2;
			subLen = max * 2;
		}
		start = pos - max + 1;
		return s.substr(start, subLen);
	}
};
```