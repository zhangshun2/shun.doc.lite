# LeetCode-79 单词搜索（快速记忆）

## 题干
给定一个 `m x n` 的字符网格 `board` 和一个字符串 `word`。
如果 `word` 可以通过按顺序连接相邻（上下左右）格子的字母得到，则返回 `true`。
同一个格子在同一次路径中**不能重复使用**。

## 数据范围（记忆版）
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` 和 `word` 由英文字母组成

## 数据示例
- board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED" → true
- 同上 board, word = "SEE" → true
- 同上 board, word = "ABCB" → false

## Java 函数入参/出参框架
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        return false;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        char[] w = word.toCharArray();

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (dfs(board, i, j, w, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, int i, int j, char[] w, int k) {
        if (k == w.length) {
            return true;
        }
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) {
            return false;
        }
        if (board[i][j] != w[k]) {
            return false;
        }

        char saved = board[i][j];
        board[i][j] = '#';

        boolean ok = dfs(board, i + 1, j, w, k + 1)
                || dfs(board, i - 1, j, w, k + 1)
                || dfs(board, i, j + 1, w, k + 1)
                || dfs(board, i, j - 1, w, k + 1);

        board[i][j] = saved;
        return ok;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        char[] w = word.toCharArray();

        // 从每个格子当作起点尝试一次
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (dfs(board, i, j, w, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, int i, int j, char[] w, int k) {
        if (k == w.length) { // 已经匹配完 word 的所有字符
            return true;
        }

        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) {
            return false;
        }

        if (board[i][j] != w[k]) { // 当前格子字符不匹配
            return false;
        }

        char saved = board[i][j];
        board[i][j] = '#'; // 原地标记：表示本次路径里这个格子已经用过了

        boolean ok = dfs(board, i + 1, j, w, k + 1)
                || dfs(board, i - 1, j, w, k + 1)
                || dfs(board, i, j + 1, w, k + 1)
                || dfs(board, i, j - 1, w, k + 1);

        board[i][j] = saved; // 回溯：恢复现场，给其他路径使用
        return ok;
    }
}
```

