# LeetCode-295 数据流的中位数（快速记忆）

## 题干
设计一个数据结构，支持从数据流中添加整数，并在任何时候返回当前所有数字的中位数。
实现 `MedianFinder`：
- `MedianFinder()` 初始化对象
- `void addNum(int num)` 添加一个数
- `double findMedian()` 返回中位数

## 数据范围（记忆版）
- `-10^5 <= num <= 10^5`
- `addNum` 总调用次数：最多约 `5 * 10^4`

## 数据示例
- addNum(1), addNum(2), findMedian() → 1.5
- addNum(3), findMedian() → 2.0

## Java 函数入参/出参框架
```java
class MedianFinder {
    public MedianFinder() {
    }

    public void addNum(int num) {
    }

    public double findMedian() {
        return 0.0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class MedianFinder {
    private final PriorityQueue<Integer> small;
    private final PriorityQueue<Integer> large;

    public MedianFinder() {
        small = new PriorityQueue<>((a, b) -> b - a);
        large = new PriorityQueue<>();
    }

    public void addNum(int num) {
        if (small.isEmpty() || num <= small.peek()) {
            small.add(num);
        } else {
            large.add(num);
        }

        if (small.size() > large.size() + 1) {
            large.add(small.poll());
        } else if (large.size() > small.size()) {
            small.add(large.poll());
        }
    }

    public double findMedian() {
        if (small.size() > large.size()) {
            return small.peek();
        }
        return (small.peek() + large.peek()) / 2.0;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class MedianFinder {
    // small：大根堆（保存较小的一半，堆顶是这一半的最大值）
    // large：小根堆（保存较大的一半，堆顶是这一半的最小值）
    private final PriorityQueue<Integer> small;
    private final PriorityQueue<Integer> large;

    public MedianFinder() {
        small = new PriorityQueue<>((a, b) -> b - a);
        large = new PriorityQueue<>();
    }

    public void addNum(int num) {
        if (small.isEmpty() || num <= small.peek()) {
            small.add(num);
        } else {
            large.add(num);
        }

        // 平衡堆大小：保证 small 的元素个数 == large 或者多 1
        if (small.size() > large.size() + 1) {
            large.add(small.poll());
        } else if (large.size() > small.size()) {
            small.add(large.poll());
        }
    }

    public double findMedian() {
        if (small.size() > large.size()) {
            return small.peek();
        }
        return (small.peek() + large.peek()) / 2.0;
    }
}
```

