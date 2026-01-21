# LeetCode-15 三数之和（快速记忆）

## 题干
给你一个整数数组 `nums`，判断是否存在三个数 `a,b,c` 使得 `a + b + c = 0`，返回所有不重复的三元组。

## 数据范围（记忆版）
- 需要去重
- 经典最优：排序 + 固定一个数 + 双指针

## 数据示例
- nums = [-1,0,1,2,-1,-4] → [[-1,-1,2],[-1,0,1]]

## Java 函数入参/出参框架
```java
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();

        for (int first = 0; first < nums.length; first++) {
            if (first > 0 && nums[first] == nums[first - 1]) continue;
            if (nums[first] > 0) break;

            int left = first + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[first] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[first], nums[left], nums[right]));
                    int leftValue = nums[left];
                    int rightValue = nums[right];
                    while (left < right && nums[left] == leftValue) left++;
                    while (left < right && nums[right] == rightValue) right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();

        for (int first = 0; first < nums.length; first++) {
            if (first > 0 && nums[first] == nums[first - 1]) {
                continue;
            }

            if (nums[first] > 0) {
                break;
            }

            int left = first + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[first] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[first], nums[left], nums[right]));

                    int leftValue = nums[left];
                    int rightValue = nums[right];
                    while (left < right && nums[left] == leftValue) left++;
                    while (left < right && nums[right] == rightValue) right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }
}
```

