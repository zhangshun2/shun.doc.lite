# LeetCode-75 颜色分类（快速记忆）

## 题干
给你一个数组 `nums`，里面只包含 `0`、`1`、`2`，分别代表红白蓝三种颜色。

请你**原地**对它们进行排序，使得相同颜色相邻，并按照 0、1、2 的顺序排列。

## 数据范围（记忆版）
- 1 <= nums.length <= 300
- nums[i] 只会是 0/1/2

## 数据示例
- nums = [2,0,2,1,1,0] → [0,0,1,1,2,2]
- nums = [2,0,1] → [0,1,2]

## Java 函数入参/出参框架
```java
class Solution {
    public void sortColors(int[] nums) {
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public void sortColors(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int i = 0;

        while (i <= right) {
            if (nums[i] == 0) {
                swap(nums, i, left);
                left++;
                i++;
            } else if (nums[i] == 2) {
                swap(nums, i, right);
                right--;
            } else {
                i++;
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public void sortColors(int[] nums) {
        // [0..left-1] 都是 0
        int left = 0;

        // [right+1..n-1] 都是 2
        int right = nums.length - 1;

        // i 在中间扫描
        int i = 0;

        while (i <= right) {
            if (nums[i] == 0) {
                // 把 0 丢到左边区间
                swap(nums, i, left);
                left++;
                i++;
            } else if (nums[i] == 2) {
                // 把 2 丢到右边区间
                // 注意：这里 i 不能 ++，因为换过来的新数还没检查
                swap(nums, i, right);
                right--;
            } else {
                // nums[i] == 1，留在中间即可
                i++;
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

