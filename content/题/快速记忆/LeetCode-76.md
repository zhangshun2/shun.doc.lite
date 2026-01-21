# LeetCode-76 最小覆盖子串（快速记忆）

## 题干
给你两个字符串 `s` 和 `t`，返回 `s` 中包含 `t` 所有字符的最小子串。
如果 `s` 中不存在这样的子串，返回空字符串 `""`。

## 数据范围（记忆版）
- `1 <= s.length, t.length <= 10^5`
- `s` 和 `t` 由英文字母组成（可按 ASCII 处理）

## 数据示例
- s = "ADOBECODEBANC", t = "ABC" → "BANC"
- s = "a", t = "a" → "a"
- s = "a", t = "aa" → ""

## Java 函数入参/出参框架
```java
class Solution {
    public String minWindow(String s, String t) {
        return null;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public String minWindow(String s, String t) {
        int[] need = new int[128];
        int needKinds = 0;
        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            if (need[c] == 0) needKinds++;
            need[c]++;
        }

        int[] window = new int[128];
        int satisfied = 0;
        int left = 0;
        int bestL = 0;
        int bestLen = Integer.MAX_VALUE;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            window[c]++;
            if (need[c] > 0 && window[c] == need[c]) {
                satisfied++;
            }

            while (satisfied == needKinds) {
                int len = right - left + 1;
                if (len < bestLen) {
                    bestLen = len;
                    bestL = left;
                }
                char d = s.charAt(left);
                window[d]--;
                if (need[d] > 0 && window[d] < need[d]) {
                    satisfied--;
                }
                left++;
            }
        }

        return bestLen == Integer.MAX_VALUE ? "" : s.substring(bestL, bestL + bestLen);
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public String minWindow(String s, String t) {
        int[] need = new int[128]; // t 中每个字符需要多少个
        int needKinds = 0;

        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            if (need[c] == 0) {
                needKinds++;
            }
            need[c]++;
        }

        int[] window = new int[128];
        int satisfied = 0; // 目前满足了多少种字符（达到 need 的数量）

        int left = 0;
        int bestL = 0;
        int bestLen = Integer.MAX_VALUE;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            window[c]++;
            if (need[c] > 0 && window[c] == need[c]) {
                satisfied++;
            }

            // 只要窗口已经覆盖 t，就尝试收缩 left，让窗口尽量短
            while (satisfied == needKinds) {
                int len = right - left + 1;
                if (len < bestLen) {
                    bestLen = len;
                    bestL = left;
                }

                char d = s.charAt(left);
                window[d]--;
                if (need[d] > 0 && window[d] < need[d]) {
                    satisfied--;
                }
                left++;
            }
        }

        return bestLen == Integer.MAX_VALUE ? "" : s.substring(bestL, bestL + bestLen);
    }
}
```

