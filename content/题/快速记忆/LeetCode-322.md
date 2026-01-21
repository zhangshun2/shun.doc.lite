# LeetCode-322 零钱兑换（快速记忆）

## 题干
给你一个整数数组 `coins` 表示不同面额的硬币，以及一个整数 `amount` 表示总金额。
返回可以凑成总金额所需的**最少**硬币个数；如果无法凑成，返回 `-1`。
每种硬币数量无限。

## 数据范围（记忆版）
- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 2^31 - 1`
- `0 <= amount <= 10^4`

## 数据示例
- coins = [1,2,5], amount = 11 → 3（5+5+1）
- coins = [2], amount = 3 → -1
- coins = [1], amount = 0 → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int c : coins) {
                if (i - c >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - c] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public int coinChange(int[] coins, int amount) {
        // dp[i]：凑出金额 i 的最少硬币数
        int[] dp = new int[amount + 1];

        // amount+1 当作 INF：因为最差也不可能用超过 amount 个 1 元硬币（如果有 1）
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int c : coins) {
                if (i - c >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - c] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

