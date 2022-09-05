## 0015 Three Sum  
[Three Sum](https://leetcode.cn/problems/3sum/)  

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 
Example 1:

Input: nums = [-1,0,1,2,-1,-4]  
Output: [[-1,-1,2],[-1,0,1]]  
Explanation:   
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.  
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.  
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.  
The distinct triplets are [-1,0,1] and [-1,-1,2].  
Notice that the order of the output and the order of the triplets does not matter.


# Solutions  
- Double Pointers  
首先对数组进行排序，排序后固定一个数 nums[i]，再使用左右指针指向 nums[i] 后面的元素两端，数字分别为 nums[L] 和 nums[R]，计算三个数的和 sum 判断是否满足为 0，满足则添加进结果集
如果 nums[i] 大于 0，则三数之和必然无法等于 0，结束循环
如果 nums[i] == nums[i - 1]，则说明该数字重复，会导致结果重复，所以应该跳过本次循环。
当 sum = 0 时，nums[L] == nums[L + 1] 则会导致结果重复，应该跳过，L++
当 sum == 00 时，nums[R] == nums[R - 1] 则会导致结果重复，应该跳过，R--  

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        nums.sort()
        ans = list()
        # 枚举 i
        for i in range(n):
            # 需要和上一次枚举的数不相同
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            # r 对应的指针初始指向数组的最右端
            r = n - 1
            target = -nums[i]
            # 枚举 L
            for l in range(i + 1, n):
                # 需要和上一次枚举的数不相同
                if l > i + 1 and nums[l] == nums[l - 1]:
                    continue
                # 需要保证 l 的指针在 r 的指针的左侧
                while l < r and nums[l] + nums[r] > target:
                    r -= 1
                # 如果指针重合，随着 l 后续的增加
                # 就不会有满足 i+l+r=0 并且 l<r 的 r 了，可以退出循环
                if l == r:
                    break
                if nums[l] + nums[r] == target:
                    ans.append([nums[i], nums[l], nums[r]])
        return ans
```
