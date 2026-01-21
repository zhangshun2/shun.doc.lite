# LeetCode-416 分割等和子集（快速记忆）

## 题干
给你一个只包含正整数的非空数组 `nums`，判断是否可以把数组分成两个子集，使得两个子集元素和相等。

## 数据范围（记忆版）
- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

## 数据示例
- nums = [1,5,11,5] → true（[1,5,5] 和 [11]）
- nums = [1,2,3,5] → false

## Java 函数入参/出参框架
```java
class Solution {
    public boolean canPartition(int[] nums) {
        return false;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int x : nums) sum += x;
        if ((sum & 1) == 1) return false;
        int target = sum / 2;

        boolean[] dp = new boolean[target + 1];
        dp[0] = true;
        for (int x : nums) {
            for (int j = target; j >= x; j--) {
                dp[j] = dp[j] || dp[j - x];
            }
        }
        return dp[target];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int x : nums) {
            sum += x;
        }

        // 总和是奇数，无法分成两个相等整数
        if ((sum & 1) == 1) {
            return false;
        }

        int target = sum / 2;

        // dp[j]：是否能选出若干个数，使得和为 j
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;

        // 0/1 背包：每个数只能用一次，所以 j 必须从大到小遍历
        for (int x : nums) {
            for (int j = target; j >= x; j--) {
                dp[j] = dp[j] || dp[j - x];
            }
        }

        return dp[target];
    }
}
```

