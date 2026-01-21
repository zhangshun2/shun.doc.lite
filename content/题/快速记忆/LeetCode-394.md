# LeetCode-394 字符串解码（快速记忆）

## 题干
给定一个经过编码的字符串 `s`，返回它解码后的字符串。
编码规则：`k[encoded_string]` 表示 `encoded_string` 重复 `k` 次。`k` 是正整数。
编码输入保证合法，且不会出现数字直接出现在普通字符中。

## 数据范围（记忆版）
- `1 <= s.length <= 30`
- `s` 由数字、字母、`[`、`]` 组成
- 解码后长度不超过 `10^5`

## 数据示例
- s = "3[a]2[bc]" → "aaabcbc"
- s = "3[a2[c]]" → "accaccacc"
- s = "2[abc]3[cd]ef" → "abcabccdcdcdef"

## Java 函数入参/出参框架
```java
class Solution {
    public String decodeString(String s) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public String decodeString(String s) {
        Deque<Integer> countSt = new ArrayDeque<>();
        Deque<StringBuilder> strSt = new ArrayDeque<>();
        StringBuilder cur = new StringBuilder();
        int num = 0;

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch >= '0' && ch <= '9') {
                num = num * 10 + (ch - '0');
            } else if (ch == '[') {
                countSt.push(num);
                strSt.push(cur);
                cur = new StringBuilder();
                num = 0;
            } else if (ch == ']') {
                int k = countSt.pop();
                StringBuilder prev = strSt.pop();
                for (int t = 0; t < k; t++) {
                    prev.append(cur);
                }
                cur = prev;
            } else {
                cur.append(ch);
            }
        }

        return cur.toString();
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public String decodeString(String s) {
        Deque<Integer> countSt = new ArrayDeque<>();
        Deque<StringBuilder> strSt = new ArrayDeque<>();

        StringBuilder cur = new StringBuilder();
        int num = 0;

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);

            if (ch >= '0' && ch <= '9') {
                num = num * 10 + (ch - '0'); // 处理多位数
            } else if (ch == '[') {
                countSt.push(num);
                strSt.push(cur);
                cur = new StringBuilder();
                num = 0;
            } else if (ch == ']') {
                int k = countSt.pop();
                StringBuilder prev = strSt.pop();

                for (int t = 0; t < k; t++) {
                    prev.append(cur);
                }

                cur = prev;
            } else {
                cur.append(ch);
            }
        }

        return cur.toString();
    }
}
```

