# LeetCode-131 分割回文串（快速记忆）

## 题干
给你一个字符串 `s`，把它分割成一些子串，使得每个子串都是回文串。
返回 `s` 所有可能的回文分割方案。

## 数据范围（记忆版）
- `1 <= s.length <= 16`
- `s` 由小写英文字母组成

## 数据示例
- s = "aab" → [["a","a","b"],["aa","b"]]
- s = "a" → [["a"]]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<String>> partition(String s) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<String>> partition(String s) {
        int n = s.length();
        boolean[][] pal = new boolean[n][n];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                if (s.charAt(i) == s.charAt(j) && (j - i <= 2 || pal[i + 1][j - 1])) {
                    pal[i][j] = true;
                }
            }
        }

        List<List<String>> ans = new ArrayList<>();
        Deque<String> path = new ArrayDeque<>();
        dfs(s, 0, pal, path, ans);
        return ans;
    }

    private void dfs(String s, int start, boolean[][] pal, Deque<String> path, List<List<String>> ans) {
        if (start == s.length()) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for (int end = start; end < s.length(); end++) {
            if (!pal[start][end]) {
                continue;
            }
            path.addLast(s.substring(start, end + 1));
            dfs(s, end + 1, pal, path, ans);
            path.removeLast();
        }
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<String>> partition(String s) {
        int n = s.length();

        // pal[i][j] = s[i..j] 是否是回文
        boolean[][] pal = new boolean[n][n];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                if (s.charAt(i) == s.charAt(j) && (j - i <= 2 || pal[i + 1][j - 1])) {
                    pal[i][j] = true;
                }
            }
        }

        List<List<String>> ans = new ArrayList<>();
        Deque<String> path = new ArrayDeque<>();
        dfs(s, 0, pal, path, ans);
        return ans;
    }

    private void dfs(String s, int start, boolean[][] pal, Deque<String> path, List<List<String>> ans) {
        if (start == s.length()) {
            ans.add(new ArrayList<>(path));
            return;
        }

        // 枚举“第一刀”切在哪里：start..end
        for (int end = start; end < s.length(); end++) {
            if (!pal[start][end]) {
                continue; // 不是回文就不能作为一段
            }

            path.addLast(s.substring(start, end + 1));
            dfs(s, end + 1, pal, path, ans);
            path.removeLast(); // 回溯：撤销本次切分
        }
    }
}
```

