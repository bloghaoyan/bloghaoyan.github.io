---
layout: post
title: "LeetCode OJ 004 Add Two Numbers"
date: 2013-11-22 14:46
comments: true
categories: LeetCode
---
>[Add Two Numbers](http://oj.leetcode.com/problems/add-two-numbers/)

###Description:
>You are given two linked lists representing two non-negative numbers.  
>The digits are stored in reverse order and each of their nodes contain a single digit.  
>Add the two numbers and return it as a linked list.
<!--more-->
###描述：
>给定两个表示两个非负数的链表。  
>其中数字位按倒序存放，每个链表结点存放一位数字。  
>将这两个数加到一起以链表形式返回。

###Input:
>(2 -> 4 -> 3) + (5 -> 6 -> 4)

###Output:
>7 -> 0 -> 8

###思路
>* 两次遍历：  
>>第一次遍历加在一块，第二次遍历处理进位。  
>* 一次遍历：    
>>用一个变量存放进位。  

###代码

```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};
```

* 两次遍历

```cpp
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        ListNode *l = new ListNode(0);
        ListNode *p = l;
        ListNode *temp = NULL;
        while(l1 && l2) {
        	temp = new ListNode(l1->val+l2->val);
        	p->next = temp;
        	p = p->next;
        	l1 = l1->next;
        	l2 = l2->next;
        }
        while(l1) {
        	temp = new ListNode(l1->val);
        	p->next = temp;
        	p = p->next;
        	l1 = l1->next;
        }
        while(l2) {
        	temp = new ListNode(l2->val);
        	p->next = temp;
        	p = p->next;
        	l2 = l2->next;
        }
        p = l->next;
        while(p->next) {
        	if(p->val>=10) {
        		p->val %= 10;
        		p->next->val++;
        	}
        	p = p->next;
        }
        if(p->val>=10) {
        	temp = new ListNode(p->val/10);
        	p->val %= 10;
        	p->next = temp;
        }
        return l->next;
    }
};
```

* 一次遍历

```cpp
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        ListNode *l = new ListNode(0);
        ListNode *p = l;
        ListNode *temp = NULL;
        int carry = 0;
        while(l1 && l2) {
        	temp = new ListNode((l1->val+l2->val+carry)%10);
            carry = (l1->val+l2->val+carry)/10;
        	p->next = temp;
        	p = p->next;
        	l1 = l1->next;
        	l2 = l2->next;
        }
        while(l1) {
        	temp = new ListNode((l1->val+carry)%10);
            carry = (l1->val+carry)/10;
        	p->next = temp;
        	p = p->next;
        	l1 = l1->next;
        }
        while(l2) {
        	temp = new ListNode((l2->val+carry)%10);
            carry = (l2->val+carry)/10;
        	p->next = temp;
        	p = p->next;
        	l2 = l2->next;
        }
        if(carry) {
        	temp = new ListNode(carry);
        	p->next = temp;
        }
        return l->next;
    }
};
```