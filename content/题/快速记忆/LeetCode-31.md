# LeetCode-31 下一个排列（快速记忆）

## 题干
给你一个整数数组 `nums`，请你把它原地修改为**字典序**下的“下一个更大排列”。

如果不存在下一个更大排列（比如 `nums` 已经是从大到小的顺序），就把它改成最小排列（从小到大）。

## 数据范围（记忆版）
- 1 <= nums.length <= 100
- -100 <= nums[i] <= 100
- 必须原地修改，额外空间尽量 O(1)

## 数据示例
- nums = [1,2,3] → [1,3,2]
- nums = [3,2,1] → [1,2,3]
- nums = [1,1,5] → [1,5,1]

## Java 函数入参/出参框架
```java
class Solution {
    public void nextPermutation(int[] nums) {
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int i = n - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }

        if (i >= 0) {
            int j = n - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }

        reverse(nums, i + 1, n - 1);
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            swap(nums, left, right);
            left++;
            right--;
        }
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;

        // 1) 从右往左找“第一处上升”：nums[i] < nums[i+1]
        //    这个 i 是“最靠右、还能让排列变大”的位置
        int i = n - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }

        // 2) 如果找到了 i，就从右往左找第一个比 nums[i] 大的数 nums[j]，交换它们
        if (i >= 0) {
            int j = n - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }

        // 3) 把 i 右边的后缀反转成升序（变成最小），这样才是“紧挨着的下一个排列”
        reverse(nums, i + 1, n - 1);
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            swap(nums, left, right);
            left++;
            right--;
        }
    }
}
```

