## 0002 Add Two Numbers
[Add Two Numbers](https://leetcode.cn/problems/add-two-numbers/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:  
Input: l1 = [2,4,3], l2 = [5,6,4]  
Output: [7,0,8]  
Explanation: 342 + 465 = 807  

## Solutions  
$TC: O(max(m,n))$ 其中 m 和 n分别为两个链表的长度。我们要遍历两个链表的全部位置，而处理每个位置只需要 O(1) 的时间。  
$SC: O(1)$   
This question is similar to `List` related problems. The key point is to convert the number properly. We can think of the remainder method.  
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        # create a dummy node
        dummy = ListNode(0)
        # create a moveble pointe tmp
        tmp = dummy
        # sum result
        sum = 0
        while l1 or l2 or sum:
            if l1:
                sum += l1.val
                l1 = l1.next
            if l2:
                sum += l2.val
                l2 = l2.next
            # remainder
            tmp.next = ListNode(sum % 10)
            tmp = tmp.next
            # keep the carry number
            sum //= 10
        return dummy.next
```