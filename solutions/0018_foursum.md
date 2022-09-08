## 0018 Four Sum  
[Four Sum](https://leetcode.cn/problems/4sum/)  

Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n  
a, b, c, and d are distinct.  
nums[a] + nums[b] + nums[c] + nums[d] == target  
You may return the answer in any order.

 
Example 1:

Input: nums = [1,0,-1,0,-2,2], target = 0  
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]  

Example 2:

Input: nums = [2,2,2,2,2], target = 8  
Output: [[2,2,2,2]]

## Solutions  
- Double Pointers  
时间复杂度：$O(n^3)$，其中 $n$ 是数组的长度。排序的时间复杂度是 $O(nlogn)$，枚举四元组的时间复杂度是 $O(n^3)$，因此总时间复杂度为 $O(n^3 + nlogn)=O(n^3)$。  
空间复杂度：$O(logn)$，其中 $$ 是数组的长度。空间复杂度主要取决于排序额外使用的空间。此外排序修改了输入数组 $nums$，实际情况中不一定允许，因此也可以看成使用了一个额外的数组存储了数组 $nums$ 的副本并排序，空间复杂度为 $O(n)$。   
The method of 4 sum is similar to 3 sum.   
For 3 sum: Locate the frist index `i` in the start position and then set two pointers: left and right `l = i + 1, r = n - 1`. n is the length of the nums.  
If we look at the 4 sum question, we just need to set an extra index before the `i`. Then do the loop for two pointers.  
```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        n = len(nums)
        nums.sort()
        res = []
        # 枚举四个指针i, j, l, r
        # i
        for i in range(n):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            # j
            for j in range(i + 1, n):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue
                # l
                l = j + 1
                # r
                r = n - 1
                # 指针相遇，退出循环
                while l < r: # 因为是排序过的数组
                    # 如果结果偏大，r 左移1位
                    if nums[i] + nums[j] + nums[l] + nums[r] > target:
                        r -= 1
                    # 如果结果偏小，l 右移1位
                    elif nums[i] + nums[j] + nums[l] + nums[r] < target:
                        l += 1
                    # 如果相等，添加到结果集
                    else:
                        res.append([nums[i], nums[j], nums[l], nums[r]])
                        # 去重
                        while l < r and nums[l] == nums[l + 1]: 
                            l += 1
                        while l < r and nums[r] == nums[r - 1]: 
                            r -= 1
                        # 继续下一次循环
                        l += 1
                        r -= 1
        return res
```
