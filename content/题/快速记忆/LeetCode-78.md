# LeetCode-78 子集（快速记忆）

## 题干
给你一个**不含重复元素**的整数数组 `nums`，返回它的所有子集（幂集）。
子集里元素的顺序不重要。

## 数据范围（记忆版）
- `0 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- `nums` 中元素互不相同

## 数据示例
- nums = [1,2,3] → [[],[1],[2],[3],[1,2],[1,3],[2,3],[1,2,3]]
- nums = [0] → [[],[0]]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(new ArrayList<>());
        for (int x : nums) {
            int size = ans.size();
            for (int i = 0; i < size; i++) {
                List<Integer> next = new ArrayList<>(ans.get(i));
                next.add(x);
                ans.add(next);
            }
        }
        return ans;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();

        // 一开始只有一个子集：空集
        ans.add(new ArrayList<>());

        for (int x : nums) {
            int size = ans.size();

            // 把当前已有的每个子集复制一份，并在复制品里加上 x
            for (int i = 0; i < size; i++) {
                List<Integer> next = new ArrayList<>(ans.get(i));
                next.add(x);
                ans.add(next);
            }
        }

        return ans;
    }
}
```

