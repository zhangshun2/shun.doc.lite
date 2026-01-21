# LeetCode-42 接雨水（快速记忆）

## 题干
给你一个非负整数数组 `height`，每个元素表示一个柱子的高度（宽度都为 1）。

雨水会留在柱子之间的凹槽里，请返回**能接住的雨水总量**。

## 数据范围（记忆版）
- 1 <= height.length <= 20000
- 0 <= height[i] <= 100000

## 数据示例
- height = [0,1,0,2,1,0,1,3,2,1,2,1] → 6
- height = [4,2,0,3,2,5] → 9

## Java 函数入参/出参框架
```java
class Solution {
    public int trap(int[] height) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int trap(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int leftMax = 0;
        int rightMax = 0;
        int water = 0;

        while (left < right) {
            if (height[left] <= height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    water += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    water += rightMax - height[right];
                }
                right--;
            }
        }

        return water;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int trap(int[] height) {
        int left = 0;
        int right = height.length - 1;

        int leftMax = 0;
        int rightMax = 0;

        int water = 0;

        while (left < right) {
            // 关键点：哪一侧“更矮”，就先结算哪一侧
            // 因为能接多少水，取决于两边挡板的较小值
            if (height[left] <= height[right]) {
                if (height[left] >= leftMax) {
                    // 当前位置变成新的左挡板
                    leftMax = height[left];
                } else {
                    // 左挡板更高，可以在这里接水
                    water += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    water += rightMax - height[right];
                }
                right--;
            }
        }

        return water;
    }
}
```

