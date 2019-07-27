---
title: 剑指offer——2.替换空格
date: 2019-07-27 18:24:54
tags:
	- 算法
	- 字符串
categories:
   - 剑指offer
---
### 1.题目
>请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

### 2.思路分析
&nbsp;&nbsp;&nbsp;&nbsp;拿到字符串之后，很容易想到有两种方式完成替换。第一种：从头到尾遍历，在原字符串的基础上进行替换。这种方式的缺点在于靠后的字符串会多次移动，因此对于含有O（n）个**空格字符**的字符串而言时间复杂度是O（n2）。第二种：创建一个新的字符串，并在其上进行替换。这种方式需要我们自己分配足够的内存空间。
&nbsp;&nbsp;&nbsp;&nbsp;本文采用了一种使用**从后向前遍历**实现空格替换的方法，这种方法中所有的字符串只需要移动一次，因此这个算法的时间复杂度为O（n）。总体的算法步骤如下：
<!--more-->
- 先遍历一次字符串，得到字符串中的空格个数，以及插入新字符之前的原字符串长度；
- 根据第一步的结果，计算出替换完成后新字符串的长度。新字符串长度 = 原字符串长度 + 空格个数*2；
- 给定两个指针a和b，a指向原字符串尾，b指向替换之后的字符串尾。向前移动指针a，逐个把它指向的字符复制到b指向的位置，直到碰到空格，a向前一格，b之前插入字符串"%20"，同时b向前移动3格。
- 重复第三步，直到a和b指向同一个位置。

### 3.举例说明
以"We are happy"为例，"We are happy"这个字符串的长度为14（包括结尾符号"\n"），里面有两个空格，因此替换之后字符串的长度是18。我们从字符串的尾部开始复制和替换。首先准备两个指针P1和P2，P1指向原始字符串的末尾，P2指向替换之后的字符串末尾。接下来向前移动指针P1，逐个把它指向的字符复制到P2指向的位置，直到碰到第一个空格。碰到第一个空格后，P1向前移动1格，P2位置开始向前插入字符串"%20"，同时P2向前移动3格。
![](字符串例子.jpg)

### 4.代码实现
**c++：**
```
class Solution{
public:
	void replaceSpace(char *string,int length){
    if(string == NULL || length <= 0)
    	return;
    //循环遍历数组，得到字符串的总长，以及空格的个数
    int originLength = 0;
    int numSpace = 0;
    int i = 0;
    while(string[i] != '\0')
    	{
        ++originLength;

        	if(string[i] == ' ')
            	++numSpace;

            ++i;
        }
    //得到新数组所需的字符串长度
    int newLength = originLength + numSpace*2;//新字符串长度 = 原字符串长度 + 空格个数*2；
    if(newLength >length)
    	return;

	////检索到空格，就将空格替换为‘%’‘2’‘0’
    int p1 = originLength;
    int p2 = newLength;
    while(p1 >= 0 && p2 > p1 ){
    	if(string[p1] == ' ')
        {
        	string[p2--] = '0';
            string[p2--] = '2';
            string[p2--] = '%';
        }
        else{
            string[p2--] = string[p1];
        }
        --p1;
    }
    }
};
```
**python2.7:**
```
# -*- coding:utf-8 -*-
class Solution:
    # string指代 源字符串
    def replaceSpace(self, string):
        # write code here
        return string.replace(' ', '%20')
```
































