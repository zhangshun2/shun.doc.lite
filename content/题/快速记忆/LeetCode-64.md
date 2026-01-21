# LeetCode-64 最小路径和（快速记忆）

## 题干
给你一个 `m x n` 的网格 `grid`，每个格子里有一个非负整数。

从左上角出发，每次只能向右或向下移动一步，直到到达右下角。

请你返回路径上的数字总和的最小值。

## 数据范围（记忆版）
- 1 <= m, n <= 200
- 0 <= grid[i][j] <= 200

## 数据示例
- grid = [[1,3,1],[1,5,1],[4,2,1]] → 7（路径 1→3→1→1→1）
- grid = [[1,2,3],[4,5,6]] → 12

## Java 函数入参/出参框架
```java
class Solution {
    public int minPathSum(int[][] grid) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        int[] dp = new int[n];
        dp[0] = grid[0][0];
        for (int j = 1; j < n; j++) {
            dp[j] = dp[j - 1] + grid[0][j];
        }

        for (int i = 1; i < m; i++) {
            dp[0] = dp[0] + grid[i][0];
            for (int j = 1; j < n; j++) {
                dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
            }
        }

        return dp[n - 1];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        // dp[j] 表示：当前行 i，到达 (i,j) 的最小路径和
        int[] dp = new int[n];

        // 初始化第一行：只能从左往右
        dp[0] = grid[0][0];
        for (int j = 1; j < n; j++) {
            dp[j] = dp[j - 1] + grid[0][j];
        }

        // 从第二行开始
        for (int i = 1; i < m; i++) {
            // 第一列：只能从上往下
            dp[0] = dp[0] + grid[i][0];

            for (int j = 1; j < n; j++) {
                // 来到 (i,j)：
                // - 从上面来：dp[j]
                // - 从左边来：dp[j-1]
                dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
            }
        }

        return dp[n - 1];
    }
}
```

