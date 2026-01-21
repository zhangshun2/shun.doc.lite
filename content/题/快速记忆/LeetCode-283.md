# LeetCode-283 移动零（快速记忆）

## 题干
给你一个数组 `nums`，请你把所有的 `0` 移动到数组的末尾。

要求：在不改变非零元素相对顺序的前提下，**原地**操作。

## 数据范围（记忆版）
- 1 <= nums.length <= 10000
- -2^31 <= nums[i] <= 2^31 - 1

## 数据示例
- nums = [0,1,0,3,12] → [1,3,12,0,0]
- nums = [0] → [0]

## Java 函数入参/出参框架
```java
class Solution {
    public void moveZeroes(int[] nums) {
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int write = 0;
        for (int read = 0; read < nums.length; read++) {
            if (nums[read] != 0) {
                int temp = nums[write];
                nums[write] = nums[read];
                nums[read] = temp;
                write++;
            }
        }
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public void moveZeroes(int[] nums) {
        // write：下一个“非零元素应该放到哪里”的位置
        int write = 0;

        for (int read = 0; read < nums.length; read++) {
            if (nums[read] != 0) {
                // 交换：把当前非零放到 write 位置
                int temp = nums[write];
                nums[write] = nums[read];
                nums[read] = temp;
                write++;
            }
        }
    }
}
```

