# LeetCode-1143 最长公共子序列（快速记忆）

## 题干
给你两个字符串 `text1` 和 `text2`，返回这两个字符串的最长公共子序列（LCS）的长度。
子序列不要求连续。

## 数据范围（记忆版）
- `1 <= text1.length, text2.length <= 1000`
- 字符只包含小写英文字母

## 数据示例
- text1 = "abcde", text2 = "ace" → 3（"ace"）
- text1 = "abc", text2 = "abc" → 3
- text1 = "abc", text2 = "def" → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n = text1.length();
        int m = text2.length();
        int[] dp = new int[m + 1];

        for (int i = 1; i <= n; i++) {
            int prevDiag = 0;
            for (int j = 1; j <= m; j++) {
                int saved = dp[j];
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[j] = prevDiag + 1;
                } else {
                    dp[j] = Math.max(dp[j], dp[j - 1]);
                }
                prevDiag = saved;
            }
        }

        return dp[m];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n = text1.length();
        int m = text2.length();

        // dp[j] 表示当前处理到 text1 的某一行时，LCS(text1[0..i), text2[0..j)) 的值
        int[] dp = new int[m + 1];

        for (int i = 1; i <= n; i++) {
            int prevDiag = 0; // 保存上一行上一列（dp[i-1][j-1]）

            for (int j = 1; j <= m; j++) {
                int saved = dp[j]; // 先存旧的 dp[j]，它是上一行的 dp[i-1][j]

                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[j] = prevDiag + 1;
                } else {
                    dp[j] = Math.max(dp[j], dp[j - 1]);
                }

                prevDiag = saved;
            }
        }

        return dp[m];
    }
}
```

