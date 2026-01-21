# LeetCode-35 搜索插入位置（深度提问）

## 我现在应该能回答
- 为什么这题等价于找 lowerBound（第一个 >= target 的位置）
- 为什么用右边界开区间 `right = nums.length` 更好写
- 为什么复杂度是 O(log n)

## 我还可以深入问
- 如果数组有重复元素，题目会变成什么（返回哪个位置）
- upperBound（第一个 > target）怎么写
- 二分写法有哪些常见的死循环坑

## 易错点清单
- 循环条件用 `left < right` 时，right 是开区间
- mid 要用 `left + (right-left)/2` 防溢出写法
- 返回的是 left，不是 mid

## 关联资料
- [模板索引.md](../../学习方法/模板索引.md)

