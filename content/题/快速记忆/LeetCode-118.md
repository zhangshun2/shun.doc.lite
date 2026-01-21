# LeetCode-118 杨辉三角（快速记忆）

## 题干
给你一个非负整数 `numRows`，生成杨辉三角的前 `numRows` 行。
杨辉三角规则：
- 每行的第一个和最后一个元素都是 1
- 其它位置元素 = 上一行对应位置的两个数之和

## 数据范围（记忆版）
- `1 <= numRows <= 30`

## 数据示例
- numRows = 5 → [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
- numRows = 1 → [[1]]

## Java 函数入参/出参框架
```java
import java.util.*;

class Solution {
    public List<List<Integer>> generate(int numRows) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();
        for (int r = 0; r < numRows; r++) {
            List<Integer> row = new ArrayList<>(r + 1);
            for (int c = 0; c <= r; c++) {
                if (c == 0 || c == r) {
                    row.add(1);
                } else {
                    row.add(ans.get(r - 1).get(c - 1) + ans.get(r - 1).get(c));
                }
            }
            ans.add(row);
        }
        return ans;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();

        for (int r = 0; r < numRows; r++) {
            List<Integer> row = new ArrayList<>(r + 1);

            for (int c = 0; c <= r; c++) {
                if (c == 0 || c == r) {
                    row.add(1);
                } else {
                    int a = ans.get(r - 1).get(c - 1);
                    int b = ans.get(r - 1).get(c);
                    row.add(a + b);
                }
            }

            ans.add(row);
        }

        return ans;
    }
}
```

