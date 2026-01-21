# LeetCode-238 除自身以外数组的乘积（快速记忆）

## 题干
给你一个整数数组 `nums`，请你返回一个数组 `answer`。

其中 `answer[i]` 等于 `nums` 中除了 `nums[i]` 之外其余各元素的乘积。

要求：不能使用除法，并且时间复杂度为 O(n)。

## 数据范围（记忆版）
- 2 <= nums.length <= 100000
- -30 <= nums[i] <= 30
- 保证任意元素的前缀积与后缀积都在 32 位整数范围内

## 数据示例
- nums = [1,2,3,4] → [24,12,8,6]
- nums = [-1,1,0,-3,3] → [0,0,9,0,0]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        return new int[0];
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] answer = new int[n];

        answer[0] = 1;
        for (int i = 1; i < n; i++) {
            answer[i] = answer[i - 1] * nums[i - 1];
        }

        int suffix = 1;
        for (int i = n - 1; i >= 0; i--) {
            answer[i] = answer[i] * suffix;
            suffix *= nums[i];
        }

        return answer;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] answer = new int[n];

        // answer[i] 先存“i 左边所有数的乘积”
        answer[0] = 1;
        for (int i = 1; i < n; i++) {
            answer[i] = answer[i - 1] * nums[i - 1];
        }

        // 再从右往左累乘一个 suffix：表示“i 右边所有数的乘积”
        int suffix = 1;
        for (int i = n - 1; i >= 0; i--) {
            answer[i] = answer[i] * suffix;
            suffix *= nums[i];
        }

        return answer;
    }
}
```

