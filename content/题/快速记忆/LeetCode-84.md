# LeetCode-84 柱状图中最大的矩形（快速记忆）

## 题干
给你一个数组 `heights`，表示柱状图中每个柱子的高度（每根柱子的宽度都为 1）。

请你返回柱状图中能勾勒出来的**最大矩形面积**。

## 数据范围（记忆版）
- 1 <= heights.length <= 100000
- 0 <= heights[i] <= 10000

## 数据示例
- heights = [2,1,5,6,2,3] → 10
- heights = [2,4] → 4

## Java 函数入参/出参框架
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int[] h = new int[n + 2];
        System.arraycopy(heights, 0, h, 1, n);

        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(0);

        int best = 0;
        for (int i = 1; i < h.length; i++) {
            while (h[i] < h[stack.peek()]) {
                int mid = stack.pop();
                int width = i - stack.peek() - 1;
                best = Math.max(best, h[mid] * width);
            }
            stack.push(i);
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;

        // 两边加哨兵 0：这样最后一定能把栈清空，不用写很多边界判断
        int[] h = new int[n + 2];
        System.arraycopy(heights, 0, h, 1, n);

        // 单调递增栈：栈里存下标，保证 h[stack[0]] < h[stack[1]] < ...
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(0);

        int best = 0;

        for (int i = 1; i < h.length; i++) {
            // 当前高度变小了：说明以“栈顶高度”为最矮的矩形，右边界找到了
            while (h[i] < h[stack.peek()]) {
                int mid = stack.pop();        // mid 是“最矮柱子”的下标
                int left = stack.peek();      // 弹出后新的栈顶，是左侧第一个更小的柱子
                int width = i - left - 1;     // 宽度：左右更小之间的距离
                best = Math.max(best, h[mid] * width);
            }
            stack.push(i);
        }

        return best;
    }
}
```

