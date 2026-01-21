# LeetCode-200 岛屿数量（快速记忆）

## 题干
给你一个由 `'1'`（陆地）和 `'0'`（水）组成的二维网格 `grid`。
请你计算网格中岛屿的数量。
岛屿定义：被水包围，并且通过上下左右相连的陆地组成的区域。

## 数据范围（记忆版）
- `1 <= grid.length, grid[0].length <= 300`
- `grid[i][j]` 是 `'0'` 或 `'1'`

## 数据示例
- grid = [["1","1","1","1","0"],["1","1","0","1","0"],["1","1","0","0","0"],["0","0","0","0","0"]] → 1
- grid = [["1","1","0","0","0"],["1","1","0","0","0"],["0","0","1","0","0"],["0","0","0","1","1"]] → 3

## Java 函数入参/出参框架
```java
class Solution {
    public int numIslands(char[][] grid) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    ans++;
                    dfs(grid, i, j);
                }
            }
        }
        return ans;
    }

    private void dfs(char[][] g, int i, int j) {
        if (i < 0 || i >= g.length || j < 0 || j >= g[0].length) return;
        if (g[i][j] != '1') return;
        g[i][j] = '0';
        dfs(g, i + 1, j);
        dfs(g, i - 1, j);
        dfs(g, i, j + 1);
        dfs(g, i, j - 1);
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int ans = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    ans++;
                    dfs(grid, i, j); // 把这座岛整块“淹掉”，避免重复计数
                }
            }
        }

        return ans;
    }

    private void dfs(char[][] g, int i, int j) {
        if (i < 0 || i >= g.length || j < 0 || j >= g[0].length) {
            return;
        }
        if (g[i][j] != '1') {
            return;
        }

        g[i][j] = '0'; // 标记已访问

        dfs(g, i + 1, j);
        dfs(g, i - 1, j);
        dfs(g, i, j + 1);
        dfs(g, i, j - 1);
    }
}
```

