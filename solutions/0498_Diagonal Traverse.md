## 0498 Diagonal Traverse  
[Diagonal Traverse](https://leetcode.cn/problems/diagonal-traverse/)  

Given an m x n matrix mat, return an array of all the elements of the array in a diagonal order.

Example 1:  
Input: mat = [[1,2,3],[4,5,6],[7,8,9]]  
Output: [1,2,4,7,5,3,6,8,9]  

## Solutions  
观察规律  
奇数次，x坐标 x -= 1, y坐标 y += 1
偶数次，x坐标 x += 1, y坐标 y -= 1

当第 i 条对角线从下往上遍历时，每次行索引减 1，列索引加 1，直到矩阵的边缘为止：
当 i < m 时，则此时对角线遍历的起点位置为 (i, 0)；
当 i ≥ m 时，则此时对角线遍历的起点位置为 (m - 1, i - m + 1)；

当第 i 条对角线从上往下遍历时，每次行索引加 1，列索引减 1，直到矩阵的边缘为止：
当 i < n 时，则此时对角线遍历的起点位置为 (0, i)；
当 i ≥ n 时，则此时对角线遍历的起点位置为 (i - n + 1, n - 1)；

```python
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        ans = []
        m, n = len(mat), len(mat[0])
        for i in range(m + n - 1): # 第i条对角线
            if i % 2: # 偶数次
                x = 0 if i < n else i - n + 1
                y = i if i < n else n - 1
                while x < m and y >= 0:
                    ans.append(mat[x][y])
                    x += 1
                    y -= 1
            else: # 奇数次
                x = i if i < m else m - 1
                y = 0 if i < m else i - m + 1
                while x >= 0 and y < n:
                    ans.append(mat[x][y])
                    x -= 1
                    y += 1
        return ans
```