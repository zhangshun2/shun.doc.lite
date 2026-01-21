# LeetCode-198 打家劫舍（快速记忆）

## 题干
你是一个小偷，想偷一条街上的房子。每个房子里有一定金额 `nums[i]`。

相邻的房子有报警系统：如果同一晚偷了相邻两间，就会报警。

请你返回在不触发报警的情况下，能偷到的最大金额。

## 数据范围（记忆版）
- 1 <= nums.length <= 100
- 0 <= nums[i] <= 400

## 数据示例
- nums = [1,2,3,1] → 4（偷 1 和 3）
- nums = [2,7,9,3,1] → 12（偷 2、9、1）

## Java 函数入参/出参框架
```java
class Solution {
    public int rob(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int rob(int[] nums) {
        int prev2 = 0;
        int prev1 = 0;

        for (int money : nums) {
            int cur = Math.max(prev1, prev2 + money);
            prev2 = prev1;
            prev1 = cur;
        }

        return prev1;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int rob(int[] nums) {
        // prev2 表示 dp[i-2]：偷到第 i-2 间（含）为止的最大金额
        // prev1 表示 dp[i-1]：偷到第 i-1 间（含）为止的最大金额
        int prev2 = 0;
        int prev1 = 0;

        for (int money : nums) {
            // 当前房子要么不偷（prev1），要么偷（prev2 + money）
            int cur = Math.max(prev1, prev2 + money);
            prev2 = prev1;
            prev1 = cur;
        }

        return prev1;
    }
}
```

