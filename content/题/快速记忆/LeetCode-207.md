# LeetCode-207 课程表（快速记忆）

## 题干
你总共有 `numCourses` 门课，编号 `0` 到 `numCourses-1`。
给你一个数组 `prerequisites`，其中 `prerequisites[i] = [a, b]` 表示：要学 `a` 先学 `b`。
如果你可以学完所有课程，返回 `true`，否则返回 `false`。

## 数据范围（记忆版）
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`

## 数据示例
- numCourses = 2, prerequisites = [[1,0]] → true
- numCourses = 2, prerequisites = [[1,0],[0,1]] → false

## Java 函数入参/出参框架
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        return false;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) g.add(new ArrayList<>());
        int[] indeg = new int[numCourses];

        for (int[] e : prerequisites) {
            int a = e[0], b = e[1];
            g.get(b).add(a);
            indeg[a]++;
        }

        Deque<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++) {
            if (indeg[i] == 0) q.addLast(i);
        }

        int done = 0;
        while (!q.isEmpty()) {
            int x = q.removeFirst();
            done++;
            for (int y : g.get(x)) {
                indeg[y]--;
                if (indeg[y] == 0) q.addLast(y);
            }
        }

        return done == numCourses;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // 建图：b -> a（学 a 之前要学 b）
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            g.add(new ArrayList<>());
        }

        int[] indeg = new int[numCourses]; // 入度：还有多少前置课没学完
        for (int[] e : prerequisites) {
            int a = e[0], b = e[1];
            g.get(b).add(a);
            indeg[a]++;
        }

        // Kahn 拓扑排序：从入度为 0 的课开始学
        Deque<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++) {
            if (indeg[i] == 0) {
                q.addLast(i);
            }
        }

        int done = 0;
        while (!q.isEmpty()) {
            int x = q.removeFirst();
            done++;

            for (int y : g.get(x)) {
                indeg[y]--;
                if (indeg[y] == 0) {
                    q.addLast(y);
                }
            }
        }

        // 能学完所有课 <=> 拓扑排序能取出 numCourses 个节点 <=> 图里没有环
        return done == numCourses;
    }
}
```

