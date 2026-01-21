# LeetCode-85 最大矩形（快速记忆）

## 题干
给你一个只包含 `'0'` 和 `'1'` 的二维矩阵 `matrix`。
请你找出只包含 `'1'` 的最大矩形，并返回其面积。

## 数据范围（记忆版）
- `1 <= matrix.length <= 200`
- `1 <= matrix[0].length <= 200`
- `matrix[i][j]` 是 `'0'` 或 `'1'`

## 数据示例
- matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]] → 6
- matrix = [["0"]] → 0
- matrix = [["1"]] → 1

## Java 函数入参/出参框架
```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int maximalRectangle(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[] heights = new int[n];
        int ans = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    heights[j] += 1;
                } else {
                    heights[j] = 0;
                }
            }
            ans = Math.max(ans, largestRectangleArea(heights));
        }
        return ans;
    }

    private int largestRectangleArea(int[] heights) {
        int n = heights.length;
        Deque<Integer> st = new ArrayDeque<>();
        int ans = 0;

        for (int i = 0; i <= n; i++) {
            int cur = (i == n) ? 0 : heights[i];
            while (!st.isEmpty() && heights[st.peek()] > cur) {
                int h = heights[st.pop()];
                int left = st.isEmpty() ? -1 : st.peek();
                int width = i - left - 1;
                ans = Math.max(ans, h * width);
            }
            st.push(i);
        }
        return ans;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public int maximalRectangle(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        // heights[j] 表示：以当前行 i 作为底，往上连续的 '1' 有多少个
        int[] heights = new int[n];
        int ans = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    heights[j] += 1;
                } else {
                    heights[j] = 0;
                }
            }

            // 每一行都把 heights 当作“柱状图”，求最大矩形面积
            ans = Math.max(ans, largestRectangleArea(heights));
        }

        return ans;
    }

    private int largestRectangleArea(int[] heights) {
        int n = heights.length;
        Deque<Integer> st = new ArrayDeque<>(); // 单调递增栈：存下标
        int ans = 0;

        // i 走到 n 时，用高度 0 作为哨兵，把栈里剩余的柱子全部结算
        for (int i = 0; i <= n; i++) {
            int cur = (i == n) ? 0 : heights[i];

            while (!st.isEmpty() && heights[st.peek()] > cur) {
                int h = heights[st.pop()];
                int left = st.isEmpty() ? -1 : st.peek();
                int width = i - left - 1;
                ans = Math.max(ans, h * width);
            }

            st.push(i);
        }

        return ans;
    }
}
```

