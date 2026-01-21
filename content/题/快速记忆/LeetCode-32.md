# LeetCode-32 最长有效括号（快速记忆）

## 题干
给你一个只包含 `(` 和 `)` 的字符串 `s`，请你找出**最长有效（格式正确）括号子串**的长度。

## 数据范围（记忆版）
- 0 <= s.length <= 30000
- s[i] 只会是 `(` 或 `)`

## 数据示例
- s = "(()" → 2
- s = ")()())" → 4
- s = "" → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int longestValidParentheses(String s) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int longestValidParentheses(String s) {
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(-1);
        int best = 0;

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.isEmpty()) {
                    stack.push(i);
                } else {
                    best = Math.max(best, i - stack.peek());
                }
            }
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int longestValidParentheses(String s) {
        Deque<Integer> stack = new ArrayDeque<>();

        // 栈里放的是“下标”
        // 先放一个哨兵 -1：表示“有效串之前的边界”
        stack.push(-1);

        int best = 0;

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch == '(') {
                stack.push(i);
            } else {
                // 试图用一个 '(' 来匹配当前 ')'
                stack.pop();

                if (stack.isEmpty()) {
                    // 说明从上一个边界到现在，')' 太多了，形成新的边界
                    stack.push(i);
                } else {
                    // 现在 stack.peek() 是“当前这段有效串之前的边界”
                    best = Math.max(best, i - stack.peek());
                }
            }
        }

        return best;
    }
}
```

