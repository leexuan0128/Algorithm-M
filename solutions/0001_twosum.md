## 0001 TwoSum
[TwoSum](https://leetcode.cn/problems/two-sum/)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:  
Input: nums = [2,7,11,15], target = 9  
Output: [0,1]  
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

## Solutions:  
- Brute Force  
$TC: O(n^2)$ 其中 N 是数组中的元素数量。最坏情况下数组中任意两个数都要被匹配一次。   
$SC: O(1)$   
The first solutoin is that I need to find the value and index of each element. Obviously, we can use `Brute Force`, using two layers of `For` loop to traverse the array. In this case, the time complexity is O(n^2). This method is not a best solution but can be used.
```python
class solution:
    def twosum(self, nums, target):
        for i in range(0, len(nums) - 1):
            for j in range(i + 1, len(nums)): # 每个数不能使用两次，所以是i + 1
                if nums[i] + nums[j] == target:
                    return [i, j]
```

- Hash Map  
