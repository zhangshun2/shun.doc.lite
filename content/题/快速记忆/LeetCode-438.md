# LeetCode-438 找到字符串中所有字母异位词（快速记忆）

## 题干
给你两个字符串 `s` 和 `p`，找出 `s` 中所有 `p` 的字母异位词的子串，返回这些子串的起始索引。
字母异位词：字符种类和数量都一样，但顺序可以不同。

## 数据范围（记忆版）
- `1 <= s.length, p.length <= 3 * 10^4`
- `s` 和 `p` 只包含小写英文字母

## 数据示例
- s = "cbaebabacd", p = "abc" → [0,6]
- s = "abab", p = "ab" → [0,1,2]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> ans = new ArrayList<>();
        if (s.length() < p.length()) return ans;

        int[] need = new int[26];
        for (int i = 0; i < p.length(); i++) need[p.charAt(i) - 'a']++;

        int[] win = new int[26];
        int k = p.length();

        for (int i = 0; i < s.length(); i++) {
            win[s.charAt(i) - 'a']++;
            if (i >= k) {
                win[s.charAt(i - k) - 'a']--;
            }
            if (i >= k - 1 && same(win, need)) {
                ans.add(i - k + 1);
            }
        }
        return ans;
    }

    private boolean same(int[] a, int[] b) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) return false;
        }
        return true;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> ans = new ArrayList<>();
        if (s.length() < p.length()) {
            return ans;
        }

        int[] need = new int[26];
        for (int i = 0; i < p.length(); i++) {
            need[p.charAt(i) - 'a']++;
        }

        int[] win = new int[26];
        int k = p.length();

        // 固定窗口大小为 k，在 s 上滑动
        for (int i = 0; i < s.length(); i++) {
            win[s.charAt(i) - 'a']++;

            if (i >= k) {
                win[s.charAt(i - k) - 'a']--;
            }

            if (i >= k - 1 && same(win, need)) {
                ans.add(i - k + 1);
            }
        }

        return ans;
    }

    private boolean same(int[] a, int[] b) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) {
                return false;
            }
        }
        return true;
    }
}
```

