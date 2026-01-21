# LeetCode-207 课程表

- 难度：中等
- 链接：https://leetcode.cn/problems/course-schedule/

## 问题描述
给定课程数量 `numCourses` 与前置关系 `prerequisites[i] = [a, b]`（表示学 `a` 之前必须先学 `b`），判断是否能完成所有课程。

## 题解一：官方经典（BFS 拓扑排序 / Kahn 算法）
- 思路：
  - 将依赖关系建图 `b -> a` 并统计每门课入度。
  - 将入度为 0 的课程入队，依次弹出并“学习”，对其后继课程入度减一，若变为 0 则入队。
  - 最终若学习课程数等于 `numCourses`，则无环，可完成；否则有环。
- 复杂度：时间 O(V+E)，空间 O(V+E)。

```java
import java.util.*;
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) g.add(new ArrayList<>());
        int[] indeg = new int[numCourses];
        for (int[] e : prerequisites) { // e[1] -> e[0]
            g.get(e[1]).add(e[0]);
            indeg[e[0]]++;
        }
        Deque<Integer> dq = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++) if (indeg[i] == 0) dq.offer(i);
        int learned = 0;
        while (!dq.isEmpty()) {
            int u = dq.poll(); learned++;
            for (int v : g.get(u)) {
                if (--indeg[v] == 0) dq.offer(v);
            }
        }
        return learned == numCourses;
    }
}
```

## 题解二：通用解法（DFS 有环检测）
- 标签：拓扑排序、图论、DFS、环检测
- 思路：对每个节点做 DFS，使用三色标记（0 未访问、1 访问中、2 已访问）检测回边；出现回边即存在环。

```java
import java.util.*;
class Solution2 {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) g.add(new ArrayList<>());
        for (int[] e : prerequisites) g.get(e[1]).add(e[0]);
        int[] state = new int[numCourses];
        for (int i = 0; i < numCourses; i++) {
            if (state[i] == 0 && !dfs(i, g, state)) return false;
        }
        return true;
    }
    private boolean dfs(int u, List<List<Integer>> g, int[] state) {
        state[u] = 1;
        for (int v : g.get(u)) {
            if (state[v] == 1) return false;          // 回边
            if (state[v] == 0 && !dfs(v, g, state)) return false;
        }
        state[u] = 2; return true;
    }
}
```

## 总结思路
- Kahn 算法与 DFS 三色标记均可判环；前者易于理解与实现，后者在需要拓扑序或检测具体环时也常用。

## 相关标签
- 拓扑排序、图论、DFS、BFS、环检测