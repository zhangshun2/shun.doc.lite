# LeetCode-35 搜索插入位置（快速记忆）

## 题干
给你一个**升序**数组 `nums` 和一个目标值 `target`。

如果 `target` 在数组里，返回它的下标；如果不在，返回它应该被插入的位置下标（插入后仍保持升序）。

## 数据范围（记忆版）
- 1 <= nums.length <= 10000
- -10000 <= nums[i], target <= 10000
- nums 是升序，且元素互不相同

## 数据示例
- nums = [1,3,5,6], target = 5 → 2
- nums = [1,3,5,6], target = 2 → 1
- nums = [1,3,5,6], target = 7 → 4

## Java 函数入参/出参框架
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
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
    public int searchInsert(int[] nums, int target) {
        // 目标：找到第一个 >= target 的位置（lowerBound）
        int left = 0;
        int right = nums.length; // 右边界用开区间

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                // mid 有可能就是答案，继续往左找更靠前的
                right = mid;
            } else {
                // mid 太小，答案一定在右边
                left = mid + 1;
            }
        }

        return left;
    }
}
```

