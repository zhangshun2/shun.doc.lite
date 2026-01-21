# LeetCode-153 寻找旋转排序数组中的最小值（快速记忆）

## 题干
给你一个可能经过旋转的升序数组 `nums`（元素互不相同）。
在 `O(log n)` 时间内找到并返回数组中的最小值。

## 数据范围（记忆版）
- `1 <= nums.length <= 5000`
- `-5000 <= nums[i] <= 5000`
- `nums` 中元素互不相同
- `nums` 是某个升序数组旋转得到（也可能没有旋转）

## 数据示例
- nums = [3,4,5,1,2] → 1
- nums = [4,5,6,7,0,1,2] → 0
- nums = [11,13,15,17] → 11

## Java 函数入参/出参框架
```java
class Solution {
    public int findMin(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] > nums[r]) {
                l = m + 1;
            } else {
                r = m;
            }
        }
        return nums[l];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;

        // 最小值一定在 [l, r] 里
        while (l < r) {
            int m = l + (r - l) / 2;

            // nums[m] > nums[r] 说明 m 在“左半段”（较大的那段），最小值在右边
            if (nums[m] > nums[r]) {
                l = m + 1;
            } else {
                // nums[m] <= nums[r] 说明 m 在“右半段”，最小值在左边（包含 m）
                r = m;
            }
        }

        return nums[l];
    }
}
```

