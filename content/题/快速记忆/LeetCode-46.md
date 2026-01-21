# LeetCode-46 全排列（快速记忆）

## 题干
给你一个**不含重复元素**的整数数组 `nums`，返回它的所有可能的全排列。

## 数据范围（记忆版）
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- `nums` 中元素互不相同

## 数据示例
- nums = [1,2,3] → [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
- nums = [0,1] → [[0,1],[1,0]]
- nums = [1] → [[1]]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int n = nums.length;
        List<List<Integer>> ans = new ArrayList<>();
        boolean[] used = new boolean[n];
        int[] path = new int[n];
        dfs(nums, 0, used, path, ans);
        return ans;
    }

    private void dfs(int[] nums, int idx, boolean[] used, int[] path, List<List<Integer>> ans) {
        if (idx == nums.length) {
            List<Integer> one = new ArrayList<>(nums.length);
            for (int x : path) {
                one.add(x);
            }
            ans.add(one);
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue;
            }
            used[i] = true;
            path[idx] = nums[i];
            dfs(nums, idx + 1, used, path, ans);
            used[i] = false;
        }
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int n = nums.length;

        List<List<Integer>> ans = new ArrayList<>();
        boolean[] used = new boolean[n]; // used[i] = nums[i] 是否已被放进当前排列
        int[] path = new int[n];         // path[idx] = 当前排列的第 idx 位放什么数

        dfs(nums, 0, used, path, ans);
        return ans;
    }

    private void dfs(int[] nums, int idx, boolean[] used, int[] path, List<List<Integer>> ans) {
        if (idx == nums.length) {
            List<Integer> one = new ArrayList<>(nums.length);
            for (int x : path) {
                one.add(x);
            }
            ans.add(one);
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue; // 这个数已经用过了，不能再用
            }

            used[i] = true;
            path[idx] = nums[i];

            dfs(nums, idx + 1, used, path, ans);

            used[i] = false; // 回溯：撤销选择，让别的分支能用它
        }
    }
}
```

