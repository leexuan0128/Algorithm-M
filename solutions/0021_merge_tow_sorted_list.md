## 0021 Merge Two Sorted Listed
[Merge Two Sorted Listed](https://leetcode.cn/problems/merge-two-sorted-lists/)  

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

Example  
Input: list1 = [1,2,4], list2 = [1,3,4]  
Output: [1,1,2,3,4,4]  

## Solutions  
- Brute Force  
$TC: O(M + N)$  
$SC: O(1)$  
We can define a dummy node `dummy = ListNode(-1)` first. Use a `pre` pointer to point the dummy. Compare the val of the l1 with l2, storing the smaller val to the dummy (move the pre pointer to comparison result): `pre.next = result`  
Judge the tail node then, `pre.next = list2 if list1 is None else list1`  

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(-1)
        pre = dummy
        while (list1 != None and list2 != None):
            if list1.val < list2.val:
                pre.next = list1
                list1 = list1.next
            else:
                pre.next = list2
                list2 = list2.next
            pre = pre.next
        pre.next = list2 if list1 is None else list1
        return dummy.next
```  

- Recursion  
$TC: O(M+N)$  
$SC: O(M+N)$  
Termination condition: When both linkedlists are empty, it means that we have completed merging the list.   
How to recurse: we decide which header of L1 or L2 is smaller, and then the next pointer of the smaller node points to the result of merging the rest of the nodes.  


```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2  # 终止条件，直到两个链表都空
        if not l2: return l1
        if l1.val <= l2.val:  # 递归调用
            l1.next = self.mergeTwoLists(l1.next,l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1,l2.next)
            return l2
```