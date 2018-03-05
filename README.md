# online_code
1.在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

解题思路（python）：
把二维数组看成是n个有序的一维数组，对一维数组进行二分查找。

<code>   
            
      
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
</code>
解题思路二：
从二维数组最左下方开始查找，若比查找的数大，则往上走，反之往右走。（因为数组行从上到下递增，从左到右递增）

<code>
       
    
    def Find(self, target, array):
        j =len(array)-1
        i =0
        while i <=len(array[j])-1 and j >=0:
            if array[j][i] ==target:
                return True
            if array[j][i] > target:
                j -=1
            elif array[j][i] < target:
                i+=1
        return False
</code>

2.输入一个链表，从尾到头打印链表每个节点的值。
    
解题思路（用时比较少）：将链表原地反转，然后访问输出。(记录当前节点，前一个节点，将当前节点的下一个节点指向前向节点，这样遍历一遍则最后得到的链表是已经反转过的链表)

  
<code>
       
    class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        # write code here
        result = []
        if listNode is None:
            return result
        else:
            pre = listNode
            current = listNode.next
            pre.next = None
            while current is not None:
                behind = current.next 
                current.next = pre 
                pre = current
                current = behind
             # 输出结果   
            while pre is not None:
                result.append(pre.val)
                pre = pre.next
            return result
 </code>


