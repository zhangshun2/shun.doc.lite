# LeetCode-1 两数之和（快速记忆）

## 题干
给你一个整数数组 `nums` 和一个目标值 `target`。请找到数组中**两个数**，它们的和等于 `target`，并返回这两个数的**下标**。

## 数据范围（记忆版）
- 2 <= nums.length
- 下标只需要返回一组答案
- 同一个元素不能用两次

## 数据示例
- nums = [2, 7, 11, 15], target = 9 → [0, 1]
- nums = [3, 2, 4], target = 6 → [1, 2]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        return new int[0];
    }
}
```

## 最优解（无注释）
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> valueToIndex = new HashMap<>();
        for (int index = 0; index < nums.length; index++) {
            int value = nums[index];
            int need = target - value;
            if (valueToIndex.containsKey(need)) {
                return new int[]{valueToIndex.get(need), index};
            }
            valueToIndex.put(value, index);
        }
        return new int[0];
    }
}
```

## 最优解（有注释）
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> valueToIndex = new HashMap<>();

        for (int index = 0; index < nums.length; index++) {
            int value = nums[index];
            int need = target - value;

            if (valueToIndex.containsKey(need)) {
                return new int[]{valueToIndex.get(need), index};
            }

            valueToIndex.put(value, index);
        }

        return new int[0];
    }
}
```

