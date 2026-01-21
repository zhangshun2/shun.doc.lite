# LeetCode-11 盛最多水的容器（快速记忆）

## 题干
给你 `n` 条竖线，第 `i` 条线的高度是 `height[i]`。两条线和 x 轴围成的容器能装水，求能装的最大水量。

## 数据范围（记忆版）
- 需要 O(n) 或 O(n log n) 级别算法
- 经典最优：双指针对撞

## 数据示例
- height = [1,8,6,2,5,4,8,3,7] → 49

## Java 函数入参/出参框架
```java
class Solution {
    public int maxArea(int[] height) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int best = 0;

        while (left < right) {
            int width = right - left;
            int h = Math.min(height[left], height[right]);
            best = Math.max(best, width * h);

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return best;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int best = 0;

        while (left < right) {
            int width = right - left;
            int currentHeight = Math.min(height[left], height[right]);
            best = Math.max(best, width * currentHeight);

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return best;
    }
}
```

