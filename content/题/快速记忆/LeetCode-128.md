# LeetCode-128 最长连续序列（快速记忆）

## 题干
给你一个未排序的整数数组 `nums`，请你找出数字连续（比如 4,5,6,7）的最长序列长度。

要求：时间复杂度尽量是 O(n)。

## 数据范围（记忆版）
- 0 <= nums.length <= 100000
- -10^9 <= nums[i] <= 10^9

## 数据示例
- nums = [100,4,200,1,3,2] → 4（1,2,3,4）
- nums = [0,3,7,2,5,8,4,6,0,1] → 9（0..8）

## Java 函数入参/出参框架
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int x : nums) {
            set.add(x);
        }

        int best = 0;
        for (int x : set) {
            if (!set.contains(x - 1)) {
                int cur = x;
                int len = 1;
                while (set.contains(cur + 1)) {
                    cur++;
                    len++;
                }
                best = Math.max(best, len);
            }
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int x : nums) {
            set.add(x);
        }

        int best = 0;

        // 只从“序列起点”开始往右扩展，避免重复计算
        for (int x : set) {
            // 如果 x-1 不存在，说明 x 是一个连续序列的起点
            if (!set.contains(x - 1)) {
                int cur = x;
                int len = 1;

                while (set.contains(cur + 1)) {
                    cur++;
                    len++;
                }

                best = Math.max(best, len);
            }
        }

        return best;
    }
}
```

