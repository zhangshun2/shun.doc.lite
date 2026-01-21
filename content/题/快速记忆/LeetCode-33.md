# LeetCode-33 搜索旋转排序数组（快速记忆）

## 题干
整数数组 `nums` 原本是升序的，但在某个未知位置做了一次旋转（例如 `[0,1,2,4,5,6,7]` 旋转成 `[4,5,6,7,0,1,2]`）。

给你 `nums` 和整数 `target`，如果 `target` 存在就返回下标，否则返回 `-1`。

要求时间复杂度尽量是 O(log n)。

## 数据范围（记忆版）
- 1 <= nums.length <= 5000
- -10000 <= nums[i] <= 10000
- nums 中元素互不相同

## 数据示例
- nums = [4,5,6,7,0,1,2], target = 0 → 4
- nums = [4,5,6,7,0,1,2], target = 3 → -1
- nums = [1], target = 0 → -1

## Java 函数入参/出参框架
```java
class Solution {
    public int search(int[] nums, int target) {
        return -1;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            }

            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            }

            // 判断哪一边是“有序的”
            if (nums[left] <= nums[mid]) {
                // 左半边有序：nums[left] ... nums[mid] 是升序
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                // 右半边有序：nums[mid] ... nums[right] 是升序
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

