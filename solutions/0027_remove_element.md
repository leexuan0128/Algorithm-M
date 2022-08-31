## 0027 remove element
[remove_element](https://leetcode.cn/problems/remove-element/)

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Custom Judge:

The judge will test your solution with the following code:

```java
int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
```
If all assertions pass, then your solution will be accepted.

## Solutions:
- Fast-Slow Pointers  
We can define two pinters, a fast pointer and a slow pointer. Slow pointer will record the value we need to keep while fast pointer will search the whole list to locate the value that we need to remove. If we find the value that equals to the value we want to remove, keep the slow pointer still but move the fast pointer to right once until it find the value not equals to the val

```python
from typing import List
class Solutions():
    def remove_element(self, nums: List[int], val: int) -> int:
        slow = fast = 0 # define two pointers
        while fast < len(nums):
            if nums[fast] != val: # we need to keep it
                nums[slow] = nums[fast]
                slow += 1
            fast += 1 # if we find the value, only move fast pointer to right once
        return slow

if __name__ == "__main__":
    s = Solutions()
    print(s.remove_element([1, 2, 3, 4, 3], 3)) #answer will be 3 -> [1,2,4,4,3] The list will be [1,2,4]
```
