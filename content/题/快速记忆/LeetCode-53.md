# LeetCode-53 最大子数组和（快速记忆）

## 题干
给你一个整数数组 `nums`，请你找到一个具有最大和的**连续子数组**（至少包含一个元素），并返回这个最大和。

## 数据范围（记忆版）
- 1 <= nums.length <= 100000
- -10000 <= nums[i] <= 10000

## 数据示例
- nums = [-2,1,-3,4,-1,2,1,-5,4] → 6

## Java 函数入参/出参框架
```java
class Solution {
    public int maxSubArray(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int best = nums[0];
        int cur = nums[0];

        for (int i = 1; i < nums.length; i++) {
            cur = Math.max(nums[i], cur + nums[i]);
            best = Math.max(best, cur);
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int best = nums[0];
        int cur = nums[0];

        for (int i = 1; i < nums.length; i++) {
            // cur 表示“以 nums[i] 结尾”的最大子数组和
            // 要么从 nums[i] 重新开始，要么接在前面的 cur 后面
            cur = Math.max(nums[i], cur + nums[i]);
            best = Math.max(best, cur);
        }

        return best;
    }
}
```

