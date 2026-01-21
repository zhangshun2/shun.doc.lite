# LeetCode-51 N 皇后（快速记忆）

## 题干
在 `n x n` 的棋盘上放置 `n` 个皇后，使得任意两个皇后都不会互相攻击。
皇后会攻击同一行、同一列、同一条对角线上的棋子。
返回所有不同的解，每个解用字符串数组表示棋盘（`Q` 表示皇后，`.` 表示空位）。

## 数据范围（记忆版）
- `1 <= n <= 9`

## 数据示例
- n = 4 → 2 种解  
  [".Q..","...Q","Q...","..Q."]  
  ["..Q.","Q...","...Q",".Q.."]
- n = 1 → ["Q"]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        int[] queenCol = new int[n];
        boolean[] colUsed = new boolean[n];
        boolean[] diag1Used = new boolean[2 * n];
        boolean[] diag2Used = new boolean[2 * n];
        dfs(n, 0, queenCol, colUsed, diag1Used, diag2Used, ans);
        return ans;
    }

    private void dfs(int n, int row, int[] queenCol, boolean[] colUsed, boolean[] diag1Used, boolean[] diag2Used, List<List<String>> ans) {
        if (row == n) {
            ans.add(buildBoard(n, queenCol));
            return;
        }
        for (int col = 0; col < n; col++) {
            int d1 = row + col;
            int d2 = row - col + n;
            if (colUsed[col] || diag1Used[d1] || diag2Used[d2]) {
                continue;
            }
            queenCol[row] = col;
            colUsed[col] = true;
            diag1Used[d1] = true;
            diag2Used[d2] = true;
            dfs(n, row + 1, queenCol, colUsed, diag1Used, diag2Used, ans);
            colUsed[col] = false;
            diag1Used[d1] = false;
            diag2Used[d2] = false;
        }
    }

    private List<String> buildBoard(int n, int[] queenCol) {
        List<String> board = new ArrayList<>(n);
        for (int r = 0; r < n; r++) {
            char[] row = new char[n];
            Arrays.fill(row, '.');
            row[queenCol[r]] = 'Q';
            board.add(new String(row));
        }
        return board;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();

        int[] queenCol = new int[n];      // queenCol[row] = 该行皇后放在哪一列
        boolean[] colUsed = new boolean[n];
        boolean[] diag1Used = new boolean[2 * n]; // 主对角线：row + col
        boolean[] diag2Used = new boolean[2 * n]; // 副对角线：row - col + n

        dfs(n, 0, queenCol, colUsed, diag1Used, diag2Used, ans);
        return ans;
    }

    private void dfs(int n, int row, int[] queenCol, boolean[] colUsed, boolean[] diag1Used, boolean[] diag2Used, List<List<String>> ans) {
        if (row == n) {
            ans.add(buildBoard(n, queenCol));
            return;
        }

        for (int col = 0; col < n; col++) {
            int d1 = row + col;
            int d2 = row - col + n;

            if (colUsed[col] || diag1Used[d1] || diag2Used[d2]) {
                continue;
            }

            queenCol[row] = col;
            colUsed[col] = true;
            diag1Used[d1] = true;
            diag2Used[d2] = true;

            dfs(n, row + 1, queenCol, colUsed, diag1Used, diag2Used, ans);

            colUsed[col] = false;
            diag1Used[d1] = false;
            diag2Used[d2] = false;
        }
    }

    private List<String> buildBoard(int n, int[] queenCol) {
        List<String> board = new ArrayList<>(n);
        for (int r = 0; r < n; r++) {
            char[] row = new char[n];
            Arrays.fill(row, '.');
            row[queenCol[r]] = 'Q';
            board.add(new String(row));
        }
        return board;
    }
}
```

