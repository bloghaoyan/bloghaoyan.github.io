---
layout: post
title: "LeetCode OJ 006 ZigZag Conversion"
date: 2013-11-24 17:21
comments: true
categories: 
---
>[ZigZag Conversion 曲折转换](http://oj.leetcode.com/problems/zigzag-conversion/)

###Description:
>The string "ABCDEFGHIJKLMNOPQRSTUVWXYZ" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)  
And then read line by line: "AKUBJLTVCIMSWDHNRXEGOQYFPZ"  
Write the code that will take a string and make this conversion given a number of rows:  
string convert(string text, int nRows);  
convert("ABCDEFGHIJKLMNOPQRSTUVWXYZ", 6) should return "AKUBJLTVCIMSWDHNRXEGOQYFPZ".  

###描述：
>字符串"ABCDEFGHIJKLMNOPQRSTUVWXYZ"按给定的行数以zigzag的模式书写，如下图：![zigzag.png](../images/postImage/006_ZigZag.png)  
>然后按行读，得到字符串"AKUBJLTVCIMSWDHNRXEGOQYFPZ"  
>编程实现这种变换。  
>convert("ABCDEFGHIJKLMNOPQRSTUVWXYZ", 6) 应返回 "AKUBJLTVCIMSWDHNRXEGOQYFPZ"。  

###思路
>一个向下和斜向上组合在一块称作一个zig，则zigSize = 2*nRow-2_(特殊情况，当nRows为1时，直接返回原字符串)_。  
>每个zig的第一行和最后一行只有1个字符，其他行有2个字符。

###代码
```cpp
class Solution {
public:
	string convert(string s, int nRows) {
		// IMPORTANT: Please reset any member data you declared, as
		// the same Solution instance will be reused for each test case.
		if (s == "") {
			return "";
		} else if (nRows == 1) {
			return s;
		}
		int zigSize = 2 * nRows - 2;
		char **p = new char *[nRows];
		int nColumn = 2 * (s.size() / zigSize + 1);
		for (int i = 0; i < nRows; i++) {
			p[i] = new char[nColumn];
			for (int j = 0; j < nColumn; j++) {
				p[i][j] = '#';
			}
		}
		int row = 0;
		int column = 0;
		int j = 0;
		for (int i = 0; i < s.size(); i++) {
			j = i % zigSize;
			if (j < nRows) {
				row = j;
			} else {
				row = zigSize - j;
			}
			if (j == 0 || j == nRows - 1) {
				column = i / zigSize;
			} else {
				if (j < nRows) {
					column = (i / zigSize) * 2;
				} else {
					column = (i / zigSize) * 2 + 1;
				}
			}
			p[row][column] = s[i];
		}

		string result(s.size(), '#');
		int pResult = 0;
		for (int i = 0; i < nRows; i++) {
			for (int j = 0; j < nColumn; j++) {
				cout << p[i][j] << " ";
			}
			cout << endl;
		}
		for (int i = 0; i < nRows; i++) {
			for (int j = 0; j < nColumn; j++) {
				if (p[i][j] == '#') {
					break;
				} else {
					result[pResult++] = p[i][j];
				}
			}
		}
		return result;
	}
};
```