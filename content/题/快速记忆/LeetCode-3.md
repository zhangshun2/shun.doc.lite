# LeetCode-3 无重复字符的最长子串（快速记忆）

## 题干
给你一个字符串 `s`，请你找出其中不含有重复字符的**最长子串**的长度。

## 数据范围（记忆版）
- s 可能很长，通常需要 O(n) 做法
- 字符可能是 ASCII 或更大字符集

## 数据示例
- s = "abcabcbb" → 3（"abc"）
- s = "bbbbb" → 1（"b"）
- s = "pwwkew" → 3（"wke"）

## Java 函数入参/出参框架
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> lastIndex = new HashMap<>();
        int left = 0;
        int best = 0;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            if (lastIndex.containsKey(c) && lastIndex.get(c) >= left) {
                left = lastIndex.get(c) + 1;
            }
            lastIndex.put(c, right);
            best = Math.max(best, right - left + 1);
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> lastIndex = new HashMap<>();

        int left = 0;
        int best = 0;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);

            if (lastIndex.containsKey(c)) {
                int previous = lastIndex.get(c);
                if (previous >= left) {
                    left = previous + 1;
                }
            }

            lastIndex.put(c, right);
            best = Math.max(best, right - left + 1);
        }

        return best;
    }
}
```

