## Reverse LinkedList
[Reverse LinkedList](https://leetcode.cn/problems/reverse-linked-list/)  

Given the head of a singly linked list, reverse the list, and return the reversed list.

Input: head = [1,2,3,4,5]  
Output: [5,4,3,2,1]  

## Solutions  
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 在头节点前定义一个pre空节点
        # 然后让头节点指向pre空节点
        # pre移动到cur，cur移动到cur.next
        # 最后return pre 或者 head = pre
        pre, cur = None, head
        while cur:
            cur.next, pre, cur = pre, cur, cur.next
        return pre
```
