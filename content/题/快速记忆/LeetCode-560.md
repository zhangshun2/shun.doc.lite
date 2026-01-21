# LeetCode-560 和为 K 的子数组（快速记忆）

## 题干
给你一个整数数组 `nums` 和一个整数 `k`，返回数组中和为 `k` 的连续子数组的个数。

## 数据范围（记忆版）
- `1 <= nums.length <= 2 * 10^4`
- `-1000 <= nums[i] <= 1000`
- `-10^7 <= k <= 10^7`

## 数据示例
- nums = [1,1,1], k = 2 → 2
- nums = [1,2,3], k = 3 → 2

## Java 函数入参/出参框架
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> cnt = new HashMap<>();
        cnt.put(0, 1);
        int sum = 0;
        int ans = 0;
        for (int x : nums) {
            sum += x;
            ans += cnt.getOrDefault(sum - k, 0);
            cnt.put(sum, cnt.getOrDefault(sum, 0) + 1);
        }
        return ans;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public int subarraySum(int[] nums, int k) {
        // cnt[prefix] = 这个前缀和出现过多少次
        Map<Integer, Integer> cnt = new HashMap<>();
        cnt.put(0, 1); // 前缀和为 0 出现 1 次：表示“从开头开始”的子数组

        int sum = 0;
        int ans = 0;

        for (int x : nums) {
            sum += x;

            // 如果存在某个之前的前缀和 prefix，使得 sum - prefix = k
            // 那么以当前结尾的子数组就有 cnt[sum-k] 个
            ans += cnt.getOrDefault(sum - k, 0);

            cnt.put(sum, cnt.getOrDefault(sum, 0) + 1);
        }

        return ans;
    }
}
```

