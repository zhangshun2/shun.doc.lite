# LeetCode-994 腐烂的橘子（快速记忆）

## 题干
在一个 `m x n` 的网格中：
- `0` 表示空格
- `1` 表示新鲜橘子
- `2` 表示腐烂橘子
每分钟，腐烂橘子会让上下左右相邻的新鲜橘子腐烂。
返回直到没有新鲜橘子为止所需的最小分钟数；如果不可能，返回 `-1`。

## 数据范围（记忆版）
- `1 <= m, n <= 10`
- `grid[i][j]` 是 0/1/2

## 数据示例
- grid = [[2,1,1],[1,1,0],[0,1,1]] → 4
- grid = [[2,1,1],[0,1,1],[1,0,1]] → -1
- grid = [[0,2]] → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int orangesRotting(int[][] grid) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public int orangesRotting(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        Deque<int[]> q = new ArrayDeque<>();
        int fresh = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) q.addLast(new int[] { i, j });
                else if (grid[i][j] == 1) fresh++;
            }
        }

        if (fresh == 0) return 0;

        int minutes = 0;
        int[][] dirs = { {1,0},{-1,0},{0,1},{0,-1} };

        while (!q.isEmpty()) {
            int size = q.size();
            boolean changed = false;

            for (int t = 0; t < size; t++) {
                int[] cur = q.removeFirst();
                for (int[] d : dirs) {
                    int ni = cur[0] + d[0];
                    int nj = cur[1] + d[1];
                    if (ni < 0 || ni >= m || nj < 0 || nj >= n) continue;
                    if (grid[ni][nj] != 1) continue;
                    grid[ni][nj] = 2;
                    fresh--;
                    q.addLast(new int[] { ni, nj });
                    changed = true;
                }
            }

            if (changed) minutes++;
        }

        return fresh == 0 ? minutes : -1;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public int orangesRotting(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        Deque<int[]> q = new ArrayDeque<>();
        int fresh = 0;

        // 多源 BFS：把所有腐烂橘子都当成起点
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    q.addLast(new int[] { i, j });
                } else if (grid[i][j] == 1) {
                    fresh++;
                }
            }
        }

        if (fresh == 0) {
            return 0;
        }

        int minutes = 0;
        int[][] dirs = { {1,0},{-1,0},{0,1},{0,-1} };

        // 每一轮循环代表“一分钟”
        while (!q.isEmpty()) {
            int size = q.size();
            boolean changed = false;

            for (int t = 0; t < size; t++) {
                int[] cur = q.removeFirst();

                for (int[] d : dirs) {
                    int ni = cur[0] + d[0];
                    int nj = cur[1] + d[1];

                    if (ni < 0 || ni >= m || nj < 0 || nj >= n) {
                        continue;
                    }
                    if (grid[ni][nj] != 1) {
                        continue;
                    }

                    grid[ni][nj] = 2;
                    fresh--;
                    q.addLast(new int[] { ni, nj });
                    changed = true;
                }
            }

            if (changed) {
                minutes++;
            }
        }

        return fresh == 0 ? minutes : -1;
    }
}
```

