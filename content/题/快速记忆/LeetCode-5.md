# LeetCode-5 最长回文子串（快速记忆）

## 题干
给你一个字符串 `s`，请你找到 `s` 中最长的回文子串。

## 数据范围（记忆版）
- 回文判断不要每次都从头比较
- 经典最优：中心扩展，O(n^2) 时间，O(1) 额外空间

## 数据示例
- s = "babad" → "bab"（或 "aba"）
- s = "cbbd" → "bb"

## Java 函数入参/出参框架
```java
class Solution {
    public String longestPalindrome(String s) {
        return "";
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) return s;

        int bestStart = 0;
        int bestLen = 1;

        for (int center = 0; center < s.length(); center++) {
            int len1 = expand(s, center, center);
            int len2 = expand(s, center, center + 1);
            int len = Math.max(len1, len2);
            if (len > bestLen) {
                bestLen = len;
                bestStart = center - (len - 1) / 2;
            }
        }

        return s.substring(bestStart, bestStart + bestLen);
    }

    private int expand(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) return s;

        int bestStart = 0;
        int bestLen = 1;

        for (int center = 0; center < s.length(); center++) {
            int oddLen = expand(s, center, center);
            int evenLen = expand(s, center, center + 1);
            int currentBest = Math.max(oddLen, evenLen);

            if (currentBest > bestLen) {
                bestLen = currentBest;
                bestStart = center - (currentBest - 1) / 2;
            }
        }

        return s.substring(bestStart, bestStart + bestLen);
    }

    private int expand(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }
}
```

