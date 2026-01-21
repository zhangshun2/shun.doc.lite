# LeetCode-39 组合总和（快速记忆）

## 题干
给你一个**无重复元素**的整数数组 `candidates` 和一个整数 `target`。
从 `candidates` 中选一些数，使它们的和等于 `target`。
每个数字**可以被无限次选择**。返回所有不重复的组合（组合内顺序不重要）。

## 数据范围（记忆版）
- `1 <= candidates.length <= 30`
- `1 <= candidates[i] <= 200`，且互不相同
- `1 <= target <= 500`

## 数据示例
- candidates = [2,3,6,7], target = 7 → [[2,2,3],[7]]
- candidates = [2,3,5], target = 8 → [[2,2,2,2],[2,3,3],[3,5]]
- candidates = [2], target = 1 → []

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> ans = new ArrayList<>();
        Deque<Integer> path = new ArrayDeque<>();
        dfs(candidates, target, 0, path, ans);
        return ans;
    }

    private void dfs(int[] candidates, int remain, int start, Deque<Integer> path, List<List<Integer>> ans) {
        if (remain == 0) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for (int i = start; i < candidates.length; i++) {
            int x = candidates[i];
            if (x > remain) {
                break;
            }
            path.addLast(x);
            dfs(candidates, remain - x, i, path, ans);
            path.removeLast();
        }
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates); // 排序后可以用“超出就停止”来剪枝

        List<List<Integer>> ans = new ArrayList<>();
        Deque<Integer> path = new ArrayDeque<>();

        dfs(candidates, target, 0, path, ans);
        return ans;
    }

    private void dfs(int[] candidates, int remain, int start, Deque<Integer> path, List<List<Integer>> ans) {
        if (remain == 0) { // 刚好凑到 target
            ans.add(new ArrayList<>(path));
            return;
        }

        for (int i = start; i < candidates.length; i++) {
            int x = candidates[i];

            // 因为 candidates 已排序，当前 x 都超过 remain，后面的更大，也不用看了
            if (x > remain) {
                break;
            }

            path.addLast(x);

            // i 不变：表示这个数可以重复使用（无限次选择）
            dfs(candidates, remain - x, i, path, ans);

            // 回溯：撤销本层选择
            path.removeLast();
        }
    }
}
```

