# LeetCode-74 搜索二维矩阵（快速记忆）

## 题干
给你一个 `m x n` 的整数矩阵 `matrix`，满足：
- 每行元素从左到右递增
- 每行第一个元素大于前一行最后一个元素
给你一个整数 `target`，如果 `target` 在矩阵中返回 `true`，否则返回 `false`。

## 数据范围（记忆版）
- `1 <= m, n <= 100`
- `-10^4 <= matrix[i][j], target <= 10^4`

## 数据示例
- matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3 → true
- 同上 matrix, target = 13 → false

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
        int l = 0;
        int r = m * n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            int x = matrix[mid / n][mid % n];
            if (x == target) return true;
            if (x < target) l = mid + 1;
            else r = mid - 1;
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

        // 由于每行首元素 > 上一行末元素，整个矩阵等价于一个长度 m*n 的有序数组
        int l = 0;
        int r = m * n - 1;

        while (l <= r) {
            int mid = l + (r - l) / 2;

            // 把一维下标映射回二维：(mid / n, mid % n)
            int x = matrix[mid / n][mid % n];

            if (x == target) {
                return true;
            } else if (x < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }

        return false;
    }
}
```

