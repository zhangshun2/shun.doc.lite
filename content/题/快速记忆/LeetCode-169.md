# LeetCode-169 多数元素（快速记忆）

## 题干
给你一个大小为 `n` 的数组 `nums`，请你返回其中的多数元素。

多数元素是指在数组中出现次数**大于** `n/2` 的元素。题目保证多数元素一定存在。

## 数据范围（记忆版）
- 1 <= nums.length <= 50000
- -10^9 <= nums[i] <= 10^9

## 数据示例
- nums = [3,2,3] → 3
- nums = [2,2,1,1,1,2,2] → 2

## Java 函数入参/出参框架
```java
class Solution {
    public int majorityElement(int[] nums) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = 0;
        int count = 0;

        for (int x : nums) {
            if (count == 0) {
                candidate = x;
                count = 1;
            } else if (x == candidate) {
                count++;
            } else {
                count--;
            }
        }

        return candidate;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int majorityElement(int[] nums) {
        // Boyer-Moore 投票法：
        // 把“多数元素”看成 +1，把“非多数元素”看成 -1，最终多数元素会剩下
        int candidate = 0;
        int count = 0;

        for (int x : nums) {
            if (count == 0) {
                candidate = x;
                count = 1;
            } else if (x == candidate) {
                count++;
            } else {
                count--;
            }
        }

        return candidate;
    }
}
```

