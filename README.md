# online_code
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

解题思路（python）：
把二维数组看成是n个有序的一维数组，对一维数组进行二分查找。

# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        
        def binsearch(data, x):
            left = 0
            right = len(data)-1
            while left<=right:
                middle = (left+right)//2
                if data[middle] == x:
                    return True
                elif data[middle] < x:
                    left = middle+1
                else:
                    right = middle-1
            return False     
        # write code here
        for i in array:
            if binsearch(i,target):
                return True
        return False
