# LeetCode-72 编辑距离（快速记忆）

## 题干
给你两个字符串 `word1` 和 `word2`。

你可以对 `word1` 做下面三种操作：
- 插入一个字符
- 删除一个字符
- 替换一个字符

请你返回把 `word1` 变成 `word2` 所需的最少操作数。

## 数据范围（记忆版）
- 0 <= word1.length, word2.length <= 500
- word1 和 word2 由小写英文字母组成

## 数据示例
- word1 = "horse", word2 = "ros" → 3
- word1 = "intention", word2 = "execution" → 5

## Java 函数入参/出参框架
```java
class Solution {
    public int minDistance(String word1, String word2) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();

        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1]));
                }
            }
        }

        return dp[m][n];
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();

        // dp[i][j]：把 word1 的前 i 个字符，变成 word2 的前 j 个字符，最少需要多少步
        int[][] dp = new int[m + 1][n + 1];

        // word2 为空：只能删除
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        // word1 为空：只能插入
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char c1 = word1.charAt(i - 1);
                char c2 = word2.charAt(j - 1);

                if (c1 == c2) {
                    // 字符相同，不需要操作
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    // 三种操作取最小：
                    // 1) 替换：dp[i-1][j-1] + 1
                    // 2) 删除：dp[i-1][j] + 1
                    // 3) 插入：dp[i][j-1] + 1
                    dp[i][j] = 1 + Math.min(
                            dp[i - 1][j - 1],
                            Math.min(dp[i - 1][j], dp[i][j - 1])
                    );
                }
            }
        }

        return dp[m][n];
    }
}
```

