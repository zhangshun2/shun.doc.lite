# LeetCode-136 只出现一次的数字（快速记忆）

## 题干
给你一个非空整数数组 `nums`，除了某个元素只出现一次以外，其余每个元素都出现两次。

请你找出那个只出现一次的元素。

## 数据范围（记忆版）
- 1 <= nums.length <= 30000
- -30000 <= nums[i] <= 30000

## 数据示例
- nums = [2,2,1] → 1
- nums = [4,1,2,1,2] → 4

## Java 函数入参/出参框架
```java
class Solution {
    public int singleNumber(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int singleNumber(int[] nums) {
        int x = 0;
        for (int v : nums) {
            x ^= v;
        }
        return x;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int singleNumber(int[] nums) {
        // 异或性质：
        // 1) a ^ a = 0
        // 2) a ^ 0 = a
        // 3) 异或满足交换律、结合律
        int x = 0;
        for (int v : nums) {
            x ^= v;
        }
        return x;
    }
}
```

