# LeetCode-189 轮转数组（快速记忆）

## 题干
给你一个数组 `nums`，请你将数组中的元素向右轮转 `k` 个位置。

## 数据范围（记忆版）
- 1 <= nums.length <= 100000
- -2^31 <= nums[i] <= 2^31 - 1
- 0 <= k <= 100000

## 数据示例
- nums = [1,2,3,4,5,6,7], k = 3 → [5,6,7,1,2,3,4]
- nums = [-1,-100,3,99], k = 2 → [3,99,-1,-100]

## Java 函数入参/出参框架
```java
class Solution {
    public void rotate(int[] nums, int k) {
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n;

        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n;

        // 例子：nums = [1,2,3,4,5,6,7], k=3
        // 1) 反转全部 -> [7,6,5,4,3,2,1]
        // 2) 反转前 k 个 -> [5,6,7,4,3,2,1]
        // 3) 反转后 n-k 个 -> [5,6,7,1,2,3,4]
        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

