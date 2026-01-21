# LeetCode-121 买卖股票的最佳时机（快速记忆）

## 题干
给你一个数组 `prices`，`prices[i]` 表示第 `i` 天股票的价格。

你只能选择**某一天买入**，并在未来的**某一天卖出**（买在前，卖在后），最多只做一次交易。

请你返回能获得的最大利润；如果不能赚钱，返回 0。

## 数据范围（记忆版）
- 1 <= prices.length <= 100000
- 0 <= prices[i] <= 10000

## 数据示例
- prices = [7,1,5,3,6,4] → 5
- prices = [7,6,4,3,1] → 0

## Java 函数入参/出参框架
```java
class Solution {
    public int maxProfit(int[] prices) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = prices[0];
        int best = 0;

        for (int i = 1; i < prices.length; i++) {
            best = Math.max(best, prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int maxProfit(int[] prices) {
        // minPrice：到今天为止出现过的最低买入价
        int minPrice = prices[0];

        // best：到今天为止的最大利润
        int best = 0;

        for (int i = 1; i < prices.length; i++) {
            // 今天卖出能赚多少：prices[i] - 之前最低价
            best = Math.max(best, prices[i] - minPrice);

            // 更新最低价（相当于考虑“今天是否更适合买入”）
            minPrice = Math.min(minPrice, prices[i]);
        }

        return best;
    }
}
```

