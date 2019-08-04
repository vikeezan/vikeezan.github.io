---
title: 剑指offer——4.重建二叉树
date: 2019-08-04 20:18:08

---
### 1.题目
> 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
tags:
    - 算法
    - 树
categories:
   - 剑指offer
### 2.思路分析
树是一种经典的数据结构，通常有以下三种遍历方式：
- 1.前序遍历：a.先访问根节点，b.再访问左子节点，c.最后访问右子节点。
- 2.中序遍历：a.先访问左子节点，b.再访问根节点，c.最后访问右子节点。
- 3.后序遍历：a.先访问左子节点，b.再访问右子节点，c.最后访问根节点。
一般二叉树的重建最少需要两种遍历方式，前序遍历和中序遍历，或者前序遍历和后序遍历。本题目中给出的条件是前序遍历和中序遍历结果，总体的算法步骤如下：
<!--more-->
- 前序遍历中，第一个数字总是树的根节点的值；
- 根据第1步的结果，可以在中序遍历序列中确定，左子树的节点值位于根节点值的左边，右子树节点的值位于根节点值的右边；
- 剩余数字根据第1、2步递归实现。
![](二叉树例子.jpg)

### 3.代码实现
**c++：**
```
/**
    * Definition for binary tree
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   class Solution {
   public:
       TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
           if (pre.size() == 0){//若子树为空，则返回NULL
               return NULL;
           }
           //分别是前序左子树，前序又子树，中序左子树，中序右子树
           vector<int> left_pre,right_pre,left_vin,right_vin;
           //前序遍历的第一个数字必定为树的根节点
           TreeNode* head = new TreeNode(pre[0]);
           int root = 0;
           for(int i = 0;i < pre.size();i++)//找到根节点在中序遍历中的位置，在该位置前的为左子树，在该位置之后的为右子树
           {
               if(pre[0] == vin[i]){
                   root = i;
                   break;
               }
           }
           
           for(int i = 0;i < root;i++){//中序遍历中的根节点，对二叉树中的节点进行归并
               left_vin.push_back(vin[i]);
               left_pre.push_back(pre[i+1]);//前序遍历第一个数为根节点
           }
           
           for(int i = root+1;i < pre.size();i++){
               right_vin.push_back(vin[i]);
               right_pre.push_back(pre[i]);
           }
           
           //递归，对左、右子树进行下一步区分，直到找到树的叶节点
           head->left = reConstructBinaryTree(left_pre,left_vin);
           head->right = reConstructBinaryTree(right_pre,right_vin);
           return head;
       }
   };
```
**python2.7:**
```
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if len(pre) == 0:
            return None
        elif len(pre) == 1:
            return TreeNode(pre[0])
        else:
            root = TreeNode(pre[0])
            pos = tin.index(pre[0])
            root.left = self.reConstructBinaryTree(pre[1:pos+1], tin[:pos])
            root.right = self.reConstructBinaryTree(pre[pos+1:], tin[pos+1:])
        return root
```