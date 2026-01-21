# LeetCode-17 电话号码的字母组合（快速记忆）

## 题干
给你一个只包含 `2-9` 的字符串 `digits`，返回它能表示的所有字母组合。

## 数据范围（记忆版）
- 典型回溯题：每一位选择一组字母
- digits 为空时返回空列表

## 数据示例
- digits = "23" → ["ad","ae","af","bd","be","bf","cd","ce","cf"]

## Java 函数入参/出参框架
```java
import java.util.List;

class Solution {
    public List<String> letterCombinations(String digits) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    private static final String[] MAPPING = {
            "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) return result;
        backtrack(digits, 0, new StringBuilder(), result);
        return result;
    }

    private void backtrack(String digits, int index, StringBuilder path, List<String> result) {
        if (index == digits.length()) {
            result.add(path.toString());
            return;
        }
        String letters = MAPPING[digits.charAt(index) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            path.append(letters.charAt(i));
            backtrack(digits, index + 1, path, result);
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
    private static final String[] MAPPING = {
            "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
    };

    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return result;
        }

        backtrack(digits, 0, new StringBuilder(), result);
        return result;
    }

    private void backtrack(String digits, int index, StringBuilder path, List<String> result) {
        if (index == digits.length()) {
            result.add(path.toString());
            return;
        }

        String letters = MAPPING[digits.charAt(index) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            path.append(letters.charAt(i));
            backtrack(digits, index + 1, path, result);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```

