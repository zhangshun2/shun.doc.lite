# LeetCode-41 缺失的第一个正数（快速记忆）

## 题干
给你一个未排序的整数数组 `nums`，请你找出其中**没有出现的最小正整数**。

要求：时间复杂度 O(n)，并且尽量只用 O(1) 额外空间。

## 数据范围（记忆版）
- 1 <= nums.length <= 100000
- -2^31 <= nums[i] <= 2^31 - 1

## 数据示例
- nums = [1,2,0] → 3
- nums = [3,4,-1,1] → 2
- nums = [7,8,9,11,12] → 1

## Java 函数入参/出参框架
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            while (nums[i] >= 1 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                swap(nums, i, nums[i] - 1);
            }
        }

        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }

        return n + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;

        // 把 “1..n 之间的数字 x” 放到它该去的位置：下标 x-1
        // 例如：数字 1 应该在 nums[0]，数字 2 应该在 nums[1]
        for (int i = 0; i < n; i++) {
            // 只要 nums[i] 是 1..n 范围内，并且它不在正确位置，就交换过去
            while (nums[i] >= 1 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                swap(nums, i, nums[i] - 1);
            }
        }

        // 现在从左往右找第一个不满足 nums[i] == i+1 的位置
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }

        // 如果 1..n 都齐了，答案就是 n+1
        return n + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

