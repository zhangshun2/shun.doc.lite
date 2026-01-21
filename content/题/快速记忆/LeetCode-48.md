# LeetCode-48 旋转图像（快速记忆）

## 题干
给你一个 `n x n` 的二维矩阵 `matrix`，请你把它**顺时针旋转 90 度**。

要求：**必须原地旋转**，不能额外开一个同样大小的新矩阵。

## 数据范围（记忆版）
- n == matrix.length == matrix[i].length
- 1 <= n <= 20
- -1000 <= matrix[i][j] <= 1000

## 数据示例
- matrix = [[1,2,3],[4,5,6],[7,8,9]] → [[7,4,1],[8,5,2],[9,6,3]]

## Java 函数入参/出参框架
```java
class Solution {
    public void rotate(int[][] matrix) {
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for (int i = 0; i < n; i++) {
            int left = 0;
            int right = n - 1;
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // 1) 沿着主对角线翻转（转置）：matrix[i][j] <-> matrix[j][i]
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // 2) 每一行左右翻转
        for (int i = 0; i < n; i++) {
            int left = 0;
            int right = n - 1;
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}
```

