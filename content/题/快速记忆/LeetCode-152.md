# LeetCode-152 乘积最大子数组（快速记忆）

## 题干
给你一个整数数组 `nums`，请你找出乘积最大的非空连续子数组，并返回该子数组的乘积。

## 数据范围（记忆版）
- `1 <= nums.length <= 2 * 10^4`
- `-10 <= nums[i] <= 10`

## 数据示例
- nums = [2,3,-2,4] → 6
- nums = [-2,0,-1] → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int maxProduct(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int maxProduct(int[] nums) {
        int maxHere = nums[0];
        int minHere = nums[0];
        int ans = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int x = nums[i];
            int a = maxHere * x;
            int b = minHere * x;
            maxHere = Math.max(x, Math.max(a, b));
            minHere = Math.min(x, Math.min(a, b));
            ans = Math.max(ans, maxHere);
        }

        return ans;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int maxProduct(int[] nums) {
        // maxHere：以 i 结尾的子数组最大乘积
        // minHere：以 i 结尾的子数组最小乘积（因为负数会翻转正负）
        int maxHere = nums[0];
        int minHere = nums[0];
        int ans = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int x = nums[i];

            int a = maxHere * x;
            int b = minHere * x;

            maxHere = Math.max(x, Math.max(a, b));
            minHere = Math.min(x, Math.min(a, b));

            ans = Math.max(ans, maxHere);
        }

        return ans;
    }
}
```

