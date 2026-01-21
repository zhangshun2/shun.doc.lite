# LeetCode-139 单词拆分（快速记忆）

## 题干
给你一个字符串 `s` 和一个字符串列表 `wordDict`（字典）。

请你判断：`s` 能不能被拆分成若干个字典里的单词，单词可以重复使用。

## 数据范围（记忆版）
- 1 <= s.length <= 300
- 1 <= wordDict.length <= 1000
- 1 <= wordDict[i].length <= 20
- s 和 wordDict[i] 都由小写字母组成

## 数据示例
- s = "leetcode", wordDict = ["leet","code"] → true
- s = "applepenapple", wordDict = ["apple","pen"] → true
- s = "catsandog", wordDict = ["cats","dog","sand","and","cat"] → false

## Java 函数入参/出参框架
```java
import java.util.List;

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return false;
    }
}
```

## 最优解（无注释）
```java
import java.util.HashSet;
import java.util.List;
import java.util.Set;

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        dp[0] = true;

        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }
}
```

## 最优解（有注释）
```java
import java.util.HashSet;
import java.util.List;
import java.util.Set;

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);

        int n = s.length();

        // dp[i]：s 的前 i 个字符（s[0..i-1]）能不能被拆分出来
        boolean[] dp = new boolean[n + 1];
        dp[0] = true; // 空串可以“拆分成功”

        for (int i = 1; i <= n; i++) {
            // 枚举最后一个单词的切分点 j：s[j..i-1]
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }
}
```

