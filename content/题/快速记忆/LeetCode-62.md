# LeetCode-62 不同路径（快速记忆）

## 题干
一个机器人在 `m x n` 的网格里，从左上角出发（起点是 `(0,0)`），每次只能向右或者向下移动一步。

请你计算：到达右下角（终点是 `(m-1,n-1)`）一共有多少条不同的路径。

## 数据范围（记忆版）
- 1 <= m, n <= 100
- 答案保证在 32 位整数范围内

## 数据示例
- m = 3, n = 7 → 28
- m = 3, n = 2 → 3

## Java 函数入参/出参框架
```java
class Solution {
    public int uniquePaths(int m, int n) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        for (int j = 0; j < n; j++) {
            dp[j] = 1;
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] = dp[j] + dp[j - 1];
            }
        }

        return dp[n - 1];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int uniquePaths(int m, int n) {
        // dp[j] 表示：当前行 i，到达位置 (i, j) 的路径数
        // 第一行只能一直往右走，所以全是 1
        int[] dp = new int[n];
        for (int j = 0; j < n; j++) {
            dp[j] = 1;
        }

        // 从第二行开始更新
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                // 到达 (i,j) 的路：
                // - 从上面来：(i-1,j)  -> dp[j]
                // - 从左边来：(i, j-1) -> dp[j-1]
                dp[j] = dp[j] + dp[j - 1];
            }
        }

        return dp[n - 1];
    }
}
```

