# LeetCode-240 搜索二维矩阵 II（快速记忆）

## 题干
给你一个 `m x n` 的整数矩阵 `matrix`，每行从左到右递增，每列从上到下递增。
给你一个整数 `target`，如果 `target` 在矩阵中返回 `true`，否则返回 `false`。

## 数据范围（记忆版）
- `1 <= m, n <= 300`
- `-10^9 <= matrix[i][j], target <= 10^9`

## 数据示例
- matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5 → true
- 同上 matrix, target = 20 → false

## Java 函数入参/出参框架
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        return false;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        int r = 0;
        int c = n - 1;
        while (r < m && c >= 0) {
            int x = matrix[r][c];
            if (x == target) return true;
            if (x > target) c--;
            else r++;
        }
        return false;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        // 从右上角出发：
        // - 当前值 > target：往左（变小）
        // - 当前值 < target：往下（变大）
        int r = 0;
        int c = n - 1;

        while (r < m && c >= 0) {
            int x = matrix[r][c];
            if (x == target) {
                return true;
            } else if (x > target) {
                c--;
            } else {
                r++;
            }
        }

        return false;
    }
}
```

