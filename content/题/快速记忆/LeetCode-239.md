# LeetCode-239 滑动窗口最大值（快速记忆）

## 题干
给你一个整数数组 `nums` 和一个整数 `k`，有一个大小为 `k` 的滑动窗口从数组最左边移动到最右边。
每次只向右移动一位，返回每个窗口中的最大值。

## 数据范围（记忆版）
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

## 数据示例
- nums = [1,3,-1,-3,5,3,6,7], k = 3 → [3,3,5,5,6,7]
- nums = [1], k = 1 → [1]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] ans = new int[n - k + 1];
        Deque<Integer> dq = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            while (!dq.isEmpty() && dq.peekFirst() <= i - k) {
                dq.removeFirst();
            }
            while (!dq.isEmpty() && nums[dq.peekLast()] <= nums[i]) {
                dq.removeLast();
            }
            dq.addLast(i);
            if (i >= k - 1) {
                ans[i - k + 1] = nums[dq.peekFirst()];
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
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] ans = new int[n - k + 1];

        // 单调队列（递减）：队头永远是当前窗口最大值的下标
        Deque<Integer> dq = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            // 1) 把窗口外的下标弹掉
            while (!dq.isEmpty() && dq.peekFirst() <= i - k) {
                dq.removeFirst();
            }

            // 2) 保持队列递减：新元素更大就把尾部小的都弹掉
            while (!dq.isEmpty() && nums[dq.peekLast()] <= nums[i]) {
                dq.removeLast();
            }

            dq.addLast(i);

            // 3) 从第一个完整窗口开始收集答案
            if (i >= k - 1) {
                ans[i - k + 1] = nums[dq.peekFirst()];
            }
        }

        return ans;
    }
}
```

