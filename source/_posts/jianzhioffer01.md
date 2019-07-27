---
title: 剑指offer——1.二维数组中的查找
date: 2019-07-27 15:40:05
tags:
	- 算法
	- 数组
categories:
   - 剑指offer
---
### 1.题目
> 在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 2.思路
假设选定一个要查找的数字，如果在数组中任意选取一个数字来和该数字作比较，可能会导致下一次要查找的区域发生重叠。为了简化查找过程，我们可以选取每个查找区域右上角数据（左下角数据也可，原理相同）和要查找的数字进行比较。此时只会发生三种情况：
<!--more-->
- 右上角的数字等于要查找的数字。查找过程结束。
- 右上角的数字大于要查找的数字。根据该二维数组的特征，排除右上角数字所在的列。
- 右上角的数字小于要查找的数字。同理，排除右上角数字所在的行。

重复以上1~3步，如果要查找的数字不在所查找区域的右上角，那么就每一次都排除一行或者一列，逐渐缩小查找范围，直到找到要查找的数字，或者查找结果为空。
### 3.举例说明
![](数组举例.jpg)
![](查找过程.jpg)

### 4.代码实现
**c++：**
```
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int rows = array.size();//数组的行序号
        int cols = array[0].size();//数组的列序号
        if(!array.empty() && rows > 0 && cols > 0){//若数组内容非空、行列序号均大于零
            int row = 0;
            int col = cols - 1;//右上角数据的行、列序号
            while(row < rows && col >= 0){//当右上角数据存在时
                if(array[row][col] == target){
                    return true;//若两数相同，查找结束
                }
                else if(array[row][col] > target){//若右上角数字大于被查找数，行不变，列减少
                    --col;
                }
                else{
                    ++row;//若右上角数字小于被查找数，行增加，列不变
                }
            }
        }
        return false;//否则，数组中不存在被查找数，查找失败
    }
};
```
**python2.7：**
```
# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        # write code here
        rows = len(array)
        cols = len(array[0])
        if rows > 0 and cols > 0:
            row = 0
            col = cols - 1
            while row < rows and col >= 0:
                if target == array[row][col]:
                    return True
                elif target < array[row][col]:
                    col -= 1
                else:
                    row += 1
        return False
```