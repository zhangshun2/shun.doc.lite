# LeetCode-4 寻找两个正序数组的中位数（快速记忆）

## 题干
给你两个升序数组 `nums1` 和 `nums2`，请你找出它们合并后的中位数，要求时间复杂度尽量低。

## 数据范围（记忆版）
- 两个数组都可能为空，但不会同时为空
- 经典最优：对较短数组做二分，O(log(min(m, n)))

## 数据示例
- nums1 = [1, 3], nums2 = [2] → 2.0
- nums1 = [1, 2], nums2 = [3, 4] → 2.5

## Java 函数入参/出参框架
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        return 0.0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length > nums2.length) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int m = nums1.length;
        int n = nums2.length;
        int totalLeft = (m + n + 1) / 2;

        int left = 0;
        int right = m;

        while (left <= right) {
            int i = left + (right - left) / 2;
            int j = totalLeft - i;

            int nums1LeftMax = (i == 0) ? Integer.MIN_VALUE : nums1[i - 1];
            int nums1RightMin = (i == m) ? Integer.MAX_VALUE : nums1[i];
            int nums2LeftMax = (j == 0) ? Integer.MIN_VALUE : nums2[j - 1];
            int nums2RightMin = (j == n) ? Integer.MAX_VALUE : nums2[j];

            if (nums1LeftMax <= nums2RightMin && nums2LeftMax <= nums1RightMin) {
                if (((m + n) & 1) == 1) {
                    return Math.max(nums1LeftMax, nums2LeftMax);
                }
                return (Math.max(nums1LeftMax, nums2LeftMax) + Math.min(nums1RightMin, nums2RightMin)) / 2.0;
            }

            if (nums1LeftMax > nums2RightMin) {
                right = i - 1;
            } else {
                left = i + 1;
            }
        }

        return 0.0;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length > nums2.length) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int m = nums1.length;
        int n = nums2.length;

        int totalLeft = (m + n + 1) / 2;

        int left = 0;
        int right = m;

        while (left <= right) {
            int i = left + (right - left) / 2;
            int j = totalLeft - i;

            int nums1LeftMax = (i == 0) ? Integer.MIN_VALUE : nums1[i - 1];
            int nums1RightMin = (i == m) ? Integer.MAX_VALUE : nums1[i];
            int nums2LeftMax = (j == 0) ? Integer.MIN_VALUE : nums2[j - 1];
            int nums2RightMin = (j == n) ? Integer.MAX_VALUE : nums2[j];

            if (nums1LeftMax <= nums2RightMin && nums2LeftMax <= nums1RightMin) {
                if (((m + n) & 1) == 1) {
                    return Math.max(nums1LeftMax, nums2LeftMax);
                }

                int leftMax = Math.max(nums1LeftMax, nums2LeftMax);
                int rightMin = Math.min(nums1RightMin, nums2RightMin);
                return (leftMax + rightMin) / 2.0;
            }

            if (nums1LeftMax > nums2RightMin) {
                right = i - 1;
            } else {
                left = i + 1;
            }
        }

        return 0.0;
    }
}
```

