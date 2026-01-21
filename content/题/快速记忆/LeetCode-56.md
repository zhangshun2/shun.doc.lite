# LeetCode-56 合并区间（快速记忆）

## 题干
给你一个区间数组 `intervals`，其中 `intervals[i] = [starti, endi]`。

请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需要覆盖输入中的所有区间。

## 数据范围（记忆版）
- 1 <= intervals.length <= 10000
- 0 <= starti <= endi <= 10000

## 数据示例
- intervals = [[1,3],[2,6],[8,10],[15,18]] → [[1,6],[8,10],[15,18]]
- intervals = [[1,4],[4,5]] → [[1,5]]

## Java 函数入参/出参框架
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        return new int[0][];
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        List<int[]> merged = new ArrayList<>();
        int curStart = intervals[0][0];
        int curEnd = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            int start = intervals[i][0];
            int end = intervals[i][1];

            if (start <= curEnd) {
                curEnd = Math.max(curEnd, end);
            } else {
                merged.add(new int[]{curStart, curEnd});
                curStart = start;
                curEnd = end;
            }
        }

        merged.add(new int[]{curStart, curEnd});
        return merged.toArray(new int[merged.size()][]);
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public int[][] merge(int[][] intervals) {
        // 先按区间起点排序
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        List<int[]> merged = new ArrayList<>();

        int curStart = intervals[0][0];
        int curEnd = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            int start = intervals[i][0];
            int end = intervals[i][1];

            if (start <= curEnd) {
                // 有重叠：把当前区间的终点扩到更远
                curEnd = Math.max(curEnd, end);
            } else {
                // 没重叠：把上一段结果收集起来，开启新的区间
                merged.add(new int[]{curStart, curEnd});
                curStart = start;
                curEnd = end;
            }
        }

        merged.add(new int[]{curStart, curEnd});
        return merged.toArray(new int[merged.size()][]);
    }
}
```

