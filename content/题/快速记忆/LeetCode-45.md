# LeetCode-45 跳跃游戏 II（快速记忆）

## 题干
给你一个非负整数数组 `nums`，你最开始在下标 0。

`nums[i]` 表示你从位置 `i` 最多可以向右跳几步。

请你返回到达最后一个下标的**最少跳跃次数**。题目保证一定能到达最后一个下标。

## 数据范围（记忆版）
- 1 <= nums.length <= 10000
- 0 <= nums[i] <= 1000
- 一定可以到达最后一个下标

## 数据示例
- nums = [2,3,1,1,4] → 2
- nums = [2,3,0,1,4] → 2

## Java 函数入参/出参框架
```java
class Solution {
    public int jump(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int jump(int[] nums) {
        int steps = 0;
        int currentEnd = 0;
        int farthest = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);
            if (i == currentEnd) {
                steps++;
                currentEnd = farthest;
            }
        }

        return steps;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int jump(int[] nums) {
        int steps = 0;

        // currentEnd：用 steps 次跳跃，当前能覆盖到的最远边界
        int currentEnd = 0;

        // farthest：在 currentEnd 这段范围内，下一跳能到的最远位置
        int farthest = 0;

        // 遍历到倒数第二个位置即可（最后一个位置不用再跳）
        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);

            // 走到当前边界，说明必须再跳一次，才能继续往后走
            if (i == currentEnd) {
                steps++;
                currentEnd = farthest;
            }
        }

        return steps;
    }
}
```

