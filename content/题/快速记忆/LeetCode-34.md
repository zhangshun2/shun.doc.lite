# LeetCode-34 在排序数组中查找元素的第一个和最后一个位置（快速记忆）

## 题干
给你一个按**非递减**顺序排列的整数数组 `nums`，和一个目标值 `target`。

请你找出 `target` 在数组中的**起始位置**和**结束位置**，并返回 `[start, end]`。

如果数组中不存在 `target`，返回 `[-1, -1]`。

要求时间复杂度尽量是 O(log n)。

## 数据范围（记忆版）
- 0 <= nums.length <= 100000
- -1000000000 <= nums[i], target <= 1000000000
- nums 已经排序（非递减）

## 数据示例
- nums = [5,7,7,8,8,10], target = 8 → [3,4]
- nums = [5,7,7,8,8,10], target = 6 → [-1,-1]
- nums = [], target = 0 → [-1,-1]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        return new int[0];
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = lowerBound(nums, target);
        if (left == nums.length || nums[left] != target) {
            return new int[]{-1, -1};
        }
        int right = lowerBound(nums, target + 1) - 1;
        return new int[]{left, right};
    }

    private int lowerBound(int[] nums, int target) {
        int left = 0;
        int right = nums.length;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        // 找到第一个 >= target 的位置
        int left = lowerBound(nums, target);

        // left 越界或者 nums[left] 不是 target，说明 target 不存在
        if (left == nums.length || nums[left] != target) {
            return new int[]{-1, -1};
        }

        // 找到第一个 >= target+1 的位置，再往左挪一格，就是最后一个 == target 的位置
        int right = lowerBound(nums, target + 1) - 1;
        return new int[]{left, right};
    }

    // 返回数组中“第一个 >= target”的下标（lower bound）
    private int lowerBound(int[] nums, int target) {
        int left = 0;
        int right = nums.length; // 右边界用“开区间”，方便写

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

