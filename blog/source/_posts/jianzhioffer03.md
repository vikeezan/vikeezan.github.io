---
title: 剑指offer——3.从尾到头打印链表
date: 2019-08-04 19:28:56
tags:
    - 算法
    - 链表
categories:
   - 剑指offer
---
### 1.题目
> 输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

### 2.思路分析
&nbsp;&nbsp;&nbsp;&nbsp;拿到链表之后想要反向输出，最容易想到的方法可能是将指针的指向变为反向，但这样会改变原本的链表结构。所以，通常情况下我们不希望改变原本的链表结构。换个角度思考，反向输出链表，那就是经典的“先进后出”数据结构，即借助栈（stack）这种数据结构完成链表的反转。总体的算法步骤如下：
<!--more-->
- 遍历链表的节点，每经过一个节点，就将该节点放到一个栈当中；
- 遍历完整个链表过后，再从栈顶开始逐个输出节点的值赋值给新的链表；

### 3.代码实现
**c++：**
```
   /**
   *  struct ListNode {
   *        int val;
   *        struct ListNode *next;
   *        ListNode(int x) :
   *              val(x), next(NULL) {
   *        }
   *  };
   */
   class Solution {
   public:
       vector<int> printListFromTailToHead(ListNode* head) {
           stack<int> nodes;//栈
           vector<int> result;//新链表
           ListNode* node=head;//原链表
           while(node != NULL){//遍历原链表，将遍历结果给栈结构nodes
               nodes.push(node->val);
               node = node->next;
           }
           
           while(!nodes.empty()){//当栈非空时，从栈顶依次将节点输出给新链表result
               result.push_back(nodes.top());
               nodes.pop();
           }
           return result;
       }
   };
```
**python2.7:**
&nbsp;&nbsp;&nbsp;&nbsp;对于python来讲，可以直接使用列表的插入方法，每次插入数据，只插入在首位。
```
   # -*- coding:utf-8 -*-
   # class ListNode:
   #     def __init__(self, x):
   #         self.val = x
   #         self.next = None
    
   class Solution:
       # 返回从尾部到头部的列表值序列，例如[1,2,3]
       def printListFromTailToHead(self, listNode):
           # write code here
           result = []
           while listNode:
               result.insert(0, listNode.val)
               listNode = listNode.next
           return result
```