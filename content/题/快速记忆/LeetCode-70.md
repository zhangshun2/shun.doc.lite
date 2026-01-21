# LeetCode-70 爬楼梯（快速记忆）

## 题干
你正在爬楼梯。到达第 `n` 阶你可以每次爬 1 阶或 2 阶。

请你计算：有多少种不同的方法可以爬到楼顶。

## 数据范围（记忆版）
- 1 <= n <= 45

## 数据示例
- n = 2 → 2（1+1，2）
- n = 3 → 3（1+1+1，1+2，2+1）

## Java 函数入参/出参框架
```java
class Solution {
    public int climbStairs(int n) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }

        int a = 1;
        int b = 2;

        for (int i = 3; i <= n; i++) {
            int c = a + b;
            a = b;
            b = c;
        }

        return b;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int climbStairs(int n) {
        // dp[i] = dp[i-1] + dp[i-2]
        // 因为到 i 阶：要么从 i-1 走 1 步来，要么从 i-2 走 2 步来
        if (n <= 2) {
            return n;
        }

        int a = 1; // dp[1]
        int b = 2; // dp[2]

        for (int i = 3; i <= n; i++) {
            int c = a + b;
            a = b;
            b = c;
        }

        return b;
    }
}
```

