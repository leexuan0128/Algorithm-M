## 0048 Rotate Image
[Rotate Image](https://leetcode.cn/problems/rotate-image/)  

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.


Example:  
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]  
Output: [[7,4,1],[8,5,2],[9,6,3]]

## Solutions  
After observation, we can find the pattern of the element movement. The `matrix[0][0] -> matrix[0][2], matrix[0][3] -> matrix[3][3]` The rule is `matrix[i][j] -> matrix[j][n - i - 1], n = len(matrix)`  
- Add an auxiliary array to replace the number 
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        # deepcopy
        matrix_new = copy.deepcopy(matrix)
        for i in range(n):
            for j in range(n):
                matrix[j][n - i - 1] = matrix_new[i][j]
```

- Two reverses  
First flip horizonally, then flip diagonally
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        for i in range(n // 2):
            for j in range(n):
                matrix[n - i - 1][j], matrix[i][j] = matrix[i][j], matrix[n - i - 1][j]
        for i in range(n):
            for j in range(i):
                matrix[j][i], matrix[i][j] = matrix[i][j], matrix[j][i]
```