# LeetCode-22 括号生成（快速记忆）

## 题干
给你一个整数 `n`，请你生成所有**有效**的由 `n` 对括号组成的字符串。

有效的意思是：任何前缀里，`(` 的数量都不能少于 `)` 的数量，并且最终 `(` 和 `)` 的数量都刚好是 `n`。

## 数据范围（记忆版）
- 1 <= n <= 8

## 数据示例
- n = 1 → ["()"]
- n = 3 → ["((()))","(()())","(())()","()(())","()()()"]

## Java 函数入参/出参框架
```java
import java.util.List;

class Solution {
    public List<String> generateParenthesis(int n) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        StringBuilder path = new StringBuilder();
        dfs(n, 0, 0, path, result);
        return result;
    }

    private void dfs(int n, int open, int close, StringBuilder path, List<String> result) {
        if (open == n && close == n) {
            result.add(path.toString());
            return;
        }

        if (open < n) {
            path.append('(');
            dfs(n, open + 1, close, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        if (close < open) {
            path.append(')');
            dfs(n, open, close + 1, path, result);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        StringBuilder path = new StringBuilder(); // 记录当前正在拼的括号串
        dfs(n, 0, 0, path, result);
        return result;
    }

    private void dfs(int n, int open, int close, StringBuilder path, List<String> result) {
        // open：已经放了多少个 '('
        // close：已经放了多少个 ')'
        if (open == n && close == n) {
            result.add(path.toString());
            return;
        }

        if (open < n) {
            // 只要 '(' 还没用完，就可以继续放 '('
            path.append('(');
            dfs(n, open + 1, close, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        if (close < open) {
            // 只有当 ')' 的数量小于 '('，才允许放 ')'
            // 这样才能保证任何前缀里 '(' 的数量都不少于 ')'
            path.append(')');
            dfs(n, open, close + 1, path, result);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```
