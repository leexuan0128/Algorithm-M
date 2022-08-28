## 0019 Remove Nth Node From End of List
[Remove Nth Node From End of List](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)  

Given the head of a linked list, remove the nth node from the end of the list and return its head.  
Example  
Input: head = [1,2,3,4,5], n = 2  
Output: [1,2,3,5]  

## Solutions  
- Two pointers (fast and slow pointers)  
$TC: O(L)$，其中 L 是链表的长度  
$SC: O(1)$  
We assume we have dummy node before the head and we set a fast and slow pointer in the dummy head position. Then, we move the fast pointer `n` steps first. This is important as we need to find the Nth node later. Next, we move fast and slow pointer one step per movement until the `fast.next` is `None`. The node that slow pointer points is the answer.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        fast = dummy
        slow = dummy
        for _ in range(n):
            fast = fast.next
        while fast.next:
            fast = fast.next
            slow = slow.next
        # 此时fast.next为空，说明fast是尾结点
        # slow.next为倒数第n个节点
        # 下面进行删除倒数第n个节点的操作
        slow.next = slow.next.next
        return dummy.next
```

