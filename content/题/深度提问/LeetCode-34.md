# LeetCode-34 查找第一个和最后一个位置（深度提问）

## 我现在应该能回答
- 为什么要写一个“lowerBound”模板
- 为什么用 `lowerBound(target+1)-1` 能找到最后位置
- 为什么这是 O(log n) 而不是 O(n)

## 我还可以深入问
- upperBound 的写法和 lowerBound 的区别是什么
- 如果要找“第一个 > target”或者“最后一个 < target”，怎么复用模板
- 如果数组是降序，二分应该怎么改

## 易错点清单
- target 不存在时要返回 [-1,-1]
- lowerBound 的右边界最好用开区间写法（right = nums.length）
- `target + 1` 可能溢出时该怎么办（更通用的 upperBound 写法）

## 关联资料
- [模板索引.md](../../学习方法/模板索引.md)

