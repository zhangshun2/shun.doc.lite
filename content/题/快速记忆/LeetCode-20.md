# LeetCode-20 有效的括号（快速记忆）

## 题干
给你一个只包含 `()[]{}` 的字符串 `s`，判断它是否是有效括号串。

## 数据范围（记忆版）
- 典型栈：遇到左括号入栈，遇到右括号检查并出栈

## 数据示例
- s = "()" → true
- s = "(]" → false
- s = "([])" → true

## Java 函数入参/出参框架
```java
class Solution {
    public boolean isValid(String s) {
        return false;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                char top = stack.pop();
                if (c == ')' && top != '(') return false;
                if (c == ']' && top != '[') return false;
                if (c == '}' && top != '{') return false;
            }
        }
        return stack.isEmpty();
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
                continue;
            }

            if (stack.isEmpty()) {
                return false;
            }

            char top = stack.pop();
            if (c == ')' && top != '(') return false;
            if (c == ']' && top != '[') return false;
            if (c == '}' && top != '{') return false;
        }

        return stack.isEmpty();
    }
}
```

