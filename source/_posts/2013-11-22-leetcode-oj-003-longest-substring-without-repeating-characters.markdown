---
layout: post
title: "LeetCode OJ 003 Longest Substring Without Repeating Characters"
date: 2013-11-22 09:01
comments: true
categories: LeetCode
---
>[Longest Substring Without Repeating Characters](http://oj.leetcode.com/problems/longest-substring-without-repeating-characters/)

###Description:
>Given a string, find the length of the longest substring without repeating characters.  
>For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.  
<!--more-->
###描述：
>给定一个字符串，找出其中无重复字符的最长子串的长度。  
>例如，对于"abcabcbb"，无重复字符的最长子串是"abc"，它的长度是3。对于"bbbbb" ，无重复字符的最长子串是"b"，它的长度是1。  

###思路
>* 简单思路：
>>维护两个指针low和i，i一直向前走，low指向目前无重复字符的子串(*不一定是最长*)的起始位置。i每读入一个字符，查看其是否在low和i之间有重复，若有则计算目前子串长度是否比之前更长，然后low更新为重复位置+1，这种方法时间复杂度O(n<sup>2</sup>)。  
>* 更好的思路：
>>维护一个大小为256的记录表table和两个指针low和i，table记录每个已遇到的字符的索引值，i一直向前走，low指向目前无重复字符的子串(*不一定是最长*)的起始位置。i每读入一个字符，从table中查看该字符是否之前已经出现过，若出现过且原索引在low和i之间，则计算目前子串长度是否比之前更长，然后将low更新为该字符原索引+1，将该字符的索引更新为i，这种方法时间复杂度O(n)。  

###代码
* O(n<sup>2</sup>)方法
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        if(s=="") {
        	return 0;
        }
        int low = 0;
        int max = 0;
        int i=1;
        for(; i<s.size();i++) {
        	int pos = s.find(s[i], low);
        	if(pos<=i-1) {
        		if(i-low>max) {
        			max = i-low;
        		}
        		low = pos+1;
        	}
        }
        if(i-low>max) {
        	max = i-low;
        }
        return max;
    }
};
```
* O(n)方法
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        if(s=="") {
        	return 0;
        }

        int rTable[256];
        for(int i=0; i<256; i++) {
            rTable[i] = -1;
        }

        int low = -1;
        int max = 0;
        int i=0;
        for(; i<s.size(); i++) {
            if(rTable[(int)s[i]]>=low) {
                if(i-low>max) {
                    max = i-low;
                }
                low = rTable[(int)s[i]]+1;
            }
            rTable[(int)s[i]] = i;
        }

        if(i-low>max) {
            max = i-low;
        }

        return max;
    }
};
```