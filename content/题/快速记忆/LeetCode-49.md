# LeetCode-49 字母异位词分组（快速记忆）

## 题干
给你一个字符串数组 `strs`，请你把其中**字母异位词**分组后返回。

字母异位词的意思是：两个字符串包含的字母种类一样，并且每个字母出现的次数也一样，只是顺序可能不同。

## 数据范围（记忆版）
- 1 <= strs.length <= 10000
- 0 <= strs[i].length <= 100
- strs[i] 由小写英文字母组成

## 数据示例
- strs = ["eat","tea","tan","ate","nat","bat"] → [["eat","tea","ate"],["tan","nat"],["bat"]]

## Java 函数入参/出参框架
```java
import java.util.List;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> keyToGroup = new HashMap<>();

        for (String s : strs) {
            int[] count = new int[26];
            for (int i = 0; i < s.length(); i++) {
                count[s.charAt(i) - 'a']++;
            }

            StringBuilder keyBuilder = new StringBuilder();
            for (int i = 0; i < 26; i++) {
                keyBuilder.append('#');
                keyBuilder.append(count[i]);
            }
            String key = keyBuilder.toString();

            keyToGroup.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
        }

        return new ArrayList<>(keyToGroup.values());
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> keyToGroup = new HashMap<>();

        for (String s : strs) {
            // 统计每个字母出现次数
            int[] count = new int[26];
            for (int i = 0; i < s.length(); i++) {
                count[s.charAt(i) - 'a']++;
            }

            // 把次数数组变成一个唯一的 key
            // 例如 [1,0,0,...,2,...] -> "#1#0#0...#2..."
            StringBuilder keyBuilder = new StringBuilder();
            for (int i = 0; i < 26; i++) {
                keyBuilder.append('#');
                keyBuilder.append(count[i]);
            }
            String key = keyBuilder.toString();

            // key 一样的字符串，就是同一组异位词
            keyToGroup.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
        }

        return new ArrayList<>(keyToGroup.values());
    }
}
```

