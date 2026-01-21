# LeetCode-287 寻找重复数（快速记忆）

## 题干
给你一个长度为 `n + 1` 的整数数组 `nums`，其中每个整数都在 `1..n` 之间（含 1 和 n）。

数组里只有一个重复的整数，但它可能重复出现多次。请你找出这个重复数。

要求：不能修改原数组，并且只用 O(1) 额外空间。

## 数据范围（记忆版）
- 1 <= n <= 100000
- nums.length == n + 1
- 1 <= nums[i] <= n
- 只有一个数重复（可能出现多次）

## 数据示例
- nums = [1,3,4,2,2] → 2
- nums = [3,1,3,4,2] → 3

## Java 函数入参/出参框架
```java
class Solution {
    public int findDuplicate(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        int finder = nums[0];
        while (finder != slow) {
            finder = nums[finder];
            slow = nums[slow];
        }

        return finder;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int findDuplicate(int[] nums) {
        // 把数组看成“下一跳指针”：
        // 当前位置 i 会跳到 nums[i]
        // 因为 nums[i] 在 1..n，而下标有 0..n，所以一定会形成环
        int slow = nums[0];
        int fast = nums[0];

        // 1) 先用快慢指针在环里相遇
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        // 2) 再找环的入口：入口对应的数字，就是重复数
        int finder = nums[0];
        while (finder != slow) {
            finder = nums[finder];
            slow = nums[slow];
        }

        return finder;
    }
}
```

