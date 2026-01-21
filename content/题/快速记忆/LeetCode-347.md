# LeetCode-347 前 K 个高频元素（快速记忆）

## 题干
给你一个整数数组 `nums` 和一个整数 `k`，请你返回出现频率前 `k` 高的元素。

返回结果的顺序不要求固定。

## 数据范围（记忆版）
- 1 <= nums.length <= 100000
- -10000 <= nums[i] <= 10000
- 1 <= k <= 不同元素的个数

## 数据示例
- nums = [1,1,1,2,2,3], k = 2 → [1,2]
- nums = [1], k = 1 → [1]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        return new int[0];
    }
}
```

## 最优解（无注释）
```java
import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> countMap = new HashMap<>();
        for (int x : nums) {
            countMap.put(x, countMap.getOrDefault(x, 0) + 1);
        }

        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));
        for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
            minHeap.offer(new int[]{entry.getKey(), entry.getValue()});
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = minHeap.poll()[0];
        }
        return result;
    }
}
```

## 最优解（有注释）
```java
import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // 1) 统计频率
        Map<Integer, Integer> countMap = new HashMap<>();
        for (int x : nums) {
            countMap.put(x, countMap.getOrDefault(x, 0) + 1);
        }

        // 2) 用大小为 k 的小顶堆：堆顶是当前“最小的频率”
        // 堆里元素用 [num, count] 来表示
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));

        for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
            minHeap.offer(new int[]{entry.getKey(), entry.getValue()});
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        // 3) 把堆里的元素取出来就是答案（顺序不重要）
        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = minHeap.poll()[0];
        }
        return result;
    }
}
```

