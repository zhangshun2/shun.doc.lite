# LeetCode-55 跳跃游戏（快速记忆）

## 题干
给你一个非负整数数组 `nums`，你最开始站在下标 0。

数组中的每个元素 `nums[i]` 代表你在该位置最多可以向右跳的步数。

请你判断是否能够到达最后一个下标。

## 数据范围（记忆版）
- 1 <= nums.length <= 10000
- 0 <= nums[i] <= 100000

## 数据示例
- nums = [2,3,1,1,4] → true
- nums = [3,2,1,0,4] → false

## Java 函数入参/出参框架
```java
class Solution {
    public boolean canJump(int[] nums) {
        return false;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public boolean canJump(int[] nums) {
        int farthest = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > farthest) {
                return false;
            }
            farthest = Math.max(farthest, i + nums[i]);
            if (farthest >= nums.length - 1) {
                return true;
            }
        }
        return true;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public boolean canJump(int[] nums) {
        // farthest：目前能到达的最远下标
        int farthest = 0;

        for (int i = 0; i < nums.length; i++) {
            // 如果当前位置 i 已经超过 farthest，说明走不到这里，直接失败
            if (i > farthest) {
                return false;
            }

            // 用当前位置更新“最远可达”
            farthest = Math.max(farthest, i + nums[i]);

            // 如果已经能到终点，提前结束
            if (farthest >= nums.length - 1) {
                return true;
            }
        }

        return true;
    }
}
```

