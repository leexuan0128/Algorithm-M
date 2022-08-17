## 0024 Swap Nodes in Pairs  
[Swap Nodes in Pairs](https://leetcode.cn/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)  

Example  
Input: head = [1,2,3,4]  
Output: [2,1,4,3]

## Solutions:  
- Iteration  
We need to swap the each adjacent nodes in the whole linkedist other than the value of the node. We define a tmp None pointer before head. The process for example above is like:  
`tmp -> 2 1 -> 3 2 -> 1 tmp -> 4 3 -> None 4 -> 3`  
```python
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 添加一个虚拟头节点
        dummy = ListNode(next = head)
        # 定义一个临时指针tmp
        tmp = dummy
        # 循环条件是tmp以及后两个位置不为空
        while tmp and tmp.next and tmp.next.next:
            n1, n2 = tmp.next, tmp.next.next
            tmp.next = n2
            n1.next = n2.next
            n2.next = n1
            tmp = tmp.next.next
        return dummy.next
```