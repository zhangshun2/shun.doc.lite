# LeetCode-279 完全平方数（快速记忆）

## 题干
给你一个整数 `n`，返回和为 `n` 的完全平方数的最少数量。
完全平方数：`1, 4, 9, 16, ...`

## 数据范围（记忆版）
- `1 <= n <= 10^4`

## 数据示例
- n = 12 → 3（4 + 4 + 4）
- n = 13 → 2（4 + 9）

## Java 函数入参/出参框架
```java
class Solution {
    public int numSquares(int n) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE / 2);
        dp[0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int k = 1; k * k <= i; k++) {
                dp[i] = Math.min(dp[i], dp[i - k * k] + 1);
            }
        }
        return dp[n];
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public int numSquares(int n) {
        // dp[i]：凑出 i 的最少完全平方数数量
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE / 2);
        dp[0] = 0;

        for (int i = 1; i <= n; i++) {
            // 枚举最后一个平方数是 k*k
            for (int k = 1; k * k <= i; k++) {
                dp[i] = Math.min(dp[i], dp[i - k * k] + 1);
            }
        }

        return dp[n];
    }
}
```

