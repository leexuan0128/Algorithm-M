## 0001 TwoSum
[TwoSum](https://leetcode.cn/problems/two-sum/)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:  
Input: nums = [2,7,11,15], target = 9
Output: [0,1]  
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

---

## Solutions:
The first idea coming into my head is that I need to find the value and index of each element. Obviously, we can use two layers of `For` loop to traverse the array. In this case, the time complexity is O(n^2). This method is not a best solution but can be used.

- Brute Force
```python
class solution:
    def twosum(self, nums, target):
        for i in range(0, len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

- Hash Map  
