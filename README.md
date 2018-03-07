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


3. 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回.

  解题思路：根据前序遍历可得到每棵子树的根节点，中序遍历的结果总是{左子树集合}根结点{右子树集合}，然后。先根据前序遍历得到每个根节点，可以将中序遍历序列不断的划分为{左子树集合}根结点{右子树集合}，以此迭代。例如：前序遍历可知：1是根节点，由中序遍历可知{4,7,2}是它的左子树，{4，2，7}在前序遍历中2根节点，然后按此不断划分迭代。
  <code>
                  
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if len(pre) == 0:
            return None
        if len(pre) == 1:
            return TreeNode(pre[0])
        else:
            node = TreeNode(pre[0])  # 找到根节点
            node.left = self.reConstructBinaryTree(pre[1:tin.index(pre[0])+1],tin[0:tin.index(pre[0])])
            node.right = self.reConstructBinaryTree(pre[tin.index(pre[0])+1:],tin[tin.index(pre[0])+1:])
            return node
                
 </code>
   
4. 用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
       
            
解题思路：使用两个列表a 和b,push元素时往a中push,pop元素时，先将a中的元素全部pop出来并添加到b中，这样b中的序列刚好与a中相反，先push的元素在顶，后puhs的元素在底。这样队列要pop的元素就是b中最顶的元素，将b中顶部元素pop出来，然后将剩余元素都依次pop出并添加到a中，此时a中的序列刚好跟原来一样，并去掉了最底的元素，此时将从b中pop的元素返回便实现了队列的pop功能。
<code>
    
 class Solution:
        
    a = []
    b = []
    def push(self, node):
        # write code here
        self.a.append(node)
    def pop(self):
        # return xx
        vaule = None
        while self.a:
            self.b.append(self.a.pop()) #将a中的元素全部push到b中
        if self.b:
            vaule = self.b.pop()
        while self.b:
            self.a.append(self.b.pop())
        return vaule  
 </code>
 5.给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。
    
 例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}；
    
 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。
   
 解题思路：滑动窗口可用固定长度的队列来实现（当固定长度的队列的记录已满，新加入元素时会自动移出最老的元素，刚好就是滑动窗口）
 记录滑动窗口的最大值，每当滑动窗口滑动一次，即将数组的下一个元素新加入队时，若改新元素比窗口最大值大，那么新窗口的最大值就是改新元素。若新元素比原滑动窗口的最大值小，那么此时需要依次比较滑动窗口里的元素，重新找出最大值。（因为此时原滑动窗口的最大值可能会被移出）
 
 <code>
            
     def maxInWindows(self, num, size):
        # write code here
        if len(num)==0 or size ==0:
            return []
        import collections
        window = collections.deque(maxlen=size) # 创建最大长度为size的队列为滑动窗口
        maxnum = num[0]
        result = []
        for index,i in enumerate(num):
            window.append(i)
            if i >=maxnum:
                maxnum = i
            elif index>=size-1:
                maxnum = window[0]
                for j in range(len(window)-1):
                    if window[j]> maxnum:
                        maxnum = window[j]
            if index >= size-1:
                result.append(maxnum)
        return result
  </code>
 
