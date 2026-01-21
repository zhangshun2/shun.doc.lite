# LeetCode-31 下一个排列

- 难度：中等
- 链接：https://leetcode.cn/problems/next-permutation/

## 问题描述
将给定序列原地重排为字典序的下一个更大排列；如果不存在（即序列为降序），则重排为最小序（升序）。

## 题解一：官方经典（三步法）
- 思路：
  1) 从右向左找到第一对升序位置 `i`，满足 `nums[i] < nums[i+1]`；若不存在，直接反转整个数组。
  2) 再从右向左找到第一个 `j` 使 `nums[j] > nums[i]`，交换 `i` 与 `j`。
  3) 反转 `i+1..n-1` 的后缀，使之最小化。
- 复杂度：时间 O(n)，空间 O(1)。

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int i = n - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) i--;
        if (i >= 0) {
            int j = n - 1;
            while (nums[j] <= nums[i]) j--;
            swap(nums, i, j);
        }
        reverse(nums, i + 1, n - 1);
    }
    private void swap(int[] a, int i, int j) { int t = a[i]; a[i] = a[j]; a[j] = t; }
    private void reverse(int[] a, int l, int r) { while (l < r) swap(a, l++, r--); }
}
```

## 题解二：最好理解（“找可增位”）
- 标签：数组、双指针、排序
- 直觉：找到能让序列变大的最靠右位置并与右侧最小大于它的数交换，随后让右侧部分最小（升序）。

## 总结思路
- 模板稳定，注意“右侧第一个大于”和“后缀反转”两个关键细节即可。

## 相关标签
- 数组、双指针、排列构造