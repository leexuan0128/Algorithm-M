## 0328 Odd Even Linkedlist
[Odd even linkedlist](https://leetcode.cn/problems/odd-even-linked-list/)  

Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

Example 1:

Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]

## Solutions
If the linked list is empty, return the linked list directly.

For the original linked list, each index of the node is a odd number or even number. The head node is a odd node. The next node of the head node is the even node. Therefore, we can separate the odd nodes and the even nodes into a odd number linked list and an even number linked list, and then connect the even linked list after the odd number list. The merged linked list is the result linked list.

The head node of the original linked list is also the head node of the odd number linked list and the head node of the result linked list. The next node of the head is the first node of the even linked list. `Evenhead = head.next`, then Evenhead is the head node of the even linked list.

Maintain two pointer `odd` and `even` point to the odd nodes and even nodes, respectively. The odd number nodes and even nodes are separated by iteration into two linked lists. Each step is to update the odd number node first, and then update the even node.

When updating the odd number node, the next node of the odd number node needs to point to the next node of the even node, so it makes `odd.next = even.next`, and then `odd = odd.next`. At this time, `odd` becomes the next node of Even.

When updating the even node, the next node of the even node needs to point to the next node of the odd number node, so it makes `even.next = odd.next`, and then make `even = even.next`. At this time, EVEN becomes the next node of ODD.

After the above operations, the separation of a odd number node and an even number node is completed. Repeat the above operations until all nodes are separated. All nodes are separated by the separation of `even` nodes or `even.next` as empty nodes. At this time, `odd` points to the last odd number node (that is, the last node of the odd number list).

Finally, `odd.next = evenHead` connects the even linked list after the odd number linked list, that is, the merger of the odd number linked list and the even number list.  

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head: 
            return
        even_head = head.next
        odd, even = head, even_head
        while even and even.next :
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        odd.next = even_head
        return head
```