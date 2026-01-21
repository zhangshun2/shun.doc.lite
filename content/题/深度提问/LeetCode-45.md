# LeetCode-45 跳跃游戏 II（深度提问）

## 我现在应该能回答
- `currentEnd` 和 `farthest` 各表示什么
- 为什么走到 `currentEnd` 就必须 +1 次跳跃
- 为什么这个贪心能保证步数最少

## 我还可以深入问
- 如何输出“实际跳跃路径”（跳到哪些下标）
- 和 LeetCode-55（能否到达）之间有什么关系
- 如果题目不保证能到达终点，代码要怎么改

## 易错点清单
- 循环只需要到 `nums.length - 2`
- 每次遇到 `i == currentEnd` 才 steps++
- 更新 currentEnd 用 farthest，不要用 i+nums[i]

## 关联资料
- [模板索引.md](../../学习方法/模板索引.md)

