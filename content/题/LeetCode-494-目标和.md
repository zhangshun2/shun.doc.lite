# LeetCode-494 目标和

- 难度：中等
- 链接：https://leetcode.cn/problems/target-sum/

## 问题描述
给定整数数组 `nums` 和目标值 `target`，你可以给每个数字添加 `+` 或 `-` 号，计算使表达式的结果等于目标值的不同表达式个数。

## 题解一：最好理解（子集和计数 DP 转化）
- 关系式：设正号子集和为 `P`，负号子集和为 `N`，则 `P - N = target` 与 `P + N = sum(nums)`，可得 `P = (target + sum)/2`。
- 转化：统计有多少子集的和等于 `P`。若 `(sum + target)` 为奇数或 `P < 0`，返回 0。
- 复杂度：时间 O(n·P)，空间 O(P)。

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0; for (int v : nums) sum += v;
        if ((sum + target) % 2 != 0) return 0;
        int P = (sum + target) / 2;
        if (P < 0) return 0;
        int[] dp = new int[P + 1];
        dp[0] = 1;
        for (int v : nums) {
            for (int j = P; j >= v; j--) {
                dp[j] += dp[j - v];
            }
        }
        return dp[P];
    }
}
```

## 题解二：官方经典（DFS + 记忆化）
- 标签：回溯、DP 转化、记忆化搜索
- 思路：递归在每个位置选择 `+` 或 `-`，用哈希表记忆 `(i, sum)` 的结果避免重复。

```java
import java.util.*;
class Solution2 {
    Map<String, Integer> memo = new HashMap<>();
    public int findTargetSumWays(int[] nums, int target) {
        return dfs(nums, 0, 0, target);
    }
    private int dfs(int[] a, int i, int sum, int target) {
        if (i == a.length) return sum == target ? 1 : 0;
        String key = i + "#" + sum;
        if (memo.containsKey(key)) return memo.get(key);
        int ways = dfs(a, i + 1, sum + a[i], target) + dfs(a, i + 1, sum - a[i], target);
        memo.put(key, ways);
        return ways;
    }
}
```

## 总结思路
- 子集和 DP 是计数更高效的常用转化；记忆化搜索更直观但在某些数据下可能慢。

## 相关标签
- 回溯、动态规划、子集和、记忆化