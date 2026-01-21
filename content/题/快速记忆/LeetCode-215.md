# LeetCode-215 数组中的第 K 个最大元素（快速记忆）

## 题干
给你一个整数数组 `nums` 和一个整数 `k`，请你返回数组中第 `k` 个最大的元素。

注意：需要找的是排序后的第 `k` 大，而不是第 `k` 个不同的元素。

## 数据范围（记忆版）
- 1 <= nums.length <= 100000
- -10000 <= nums[i] <= 10000
- 1 <= k <= nums.length

## 数据示例
- nums = [3,2,1,5,6,4], k = 2 → 5
- nums = [3,2,3,1,2,4,5,5,6], k = 4 → 4

## Java 函数入参/出参框架
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.PriorityQueue;

class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int x : nums) {
            minHeap.offer(x);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        return minHeap.peek();
    }
}
```

## 最优解（有注释）
```java
import java.util.PriorityQueue;

class Solution {
    public int findKthLargest(int[] nums, int k) {
        // 小顶堆，堆里最多放 k 个数
        // 保证堆顶是“当前第 k 大”
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int x : nums) {
            minHeap.offer(x);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        return minHeap.peek();
    }
}
```

