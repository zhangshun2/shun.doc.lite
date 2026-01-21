# LeetCode-300 最长递增子序列（快速记忆）

## 题干
给你一个整数数组 `nums`，找到其中最长严格递增子序列的长度。
子序列不要求连续。

## 数据范围（记忆版）
- `1 <= nums.length <= 2500`
- `-10^4 <= nums[i] <= 10^4`

## 数据示例
- nums = [10,9,2,5,3,7,101,18] → 4（比如 [2,3,7,101]）
- nums = [0,1,0,3,2,3] → 4
- nums = [7,7,7,7] → 1

## Java 函数入参/出参框架
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] tails = new int[nums.length];
        int size = 0;
        for (int x : nums) {
            int l = 0, r = size;
            while (l < r) {
                int m = l + (r - l) / 2;
                if (tails[m] < x) {
                    l = m + 1;
                } else {
                    r = m;
                }
            }
            tails[l] = x;
            if (l == size) {
                size++;
            }
        }
        return size;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        // tails[i]：长度为 i+1 的递增子序列，其“末尾元素的最小可能值”
        int[] tails = new int[nums.length];
        int size = 0;

        for (int x : nums) {
            int l = 0, r = size;

            // 找到第一个 >= x 的位置，替换它，让尾巴尽量小
            while (l < r) {
                int m = l + (r - l) / 2;
                if (tails[m] < x) {
                    l = m + 1;
                } else {
                    r = m;
                }
            }

            tails[l] = x;
            if (l == size) {
                size++;
            }
        }

        return size;
    }
}
```

