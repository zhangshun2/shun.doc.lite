# LeetCode-739 每日温度（快速记忆）

## 题干
给你一个整数数组 `temperatures`，`temperatures[i]` 表示第 `i` 天的温度。

请你返回一个数组 `answer`：对每一天 `i`，`answer[i]` 是你要等多少天才会遇到更高的温度；如果之后不会升温，就填 0。

## 数据范围（记忆版）
- 1 <= temperatures.length <= 100000
- 30 <= temperatures[i] <= 100

## 数据示例
- temperatures = [73,74,75,71,69,72,76,73] → [1,1,4,2,1,1,0,0]
- temperatures = [30,40,50,60] → [1,1,1,0]

## Java 函数入参/出参框架
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        return new int[0];
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] answer = new int[n];
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                answer[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }

        return answer;
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] answer = new int[n];

        // 单调栈：栈里存“下标”
        // 从栈底到栈顶，对应的温度是递减的
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            // 当前温度更高：可以结算之前那些更低温度的“等待天数”
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                answer[prevIndex] = i - prevIndex;
            }

            // 当前天入栈，等待未来出现更高温度
            stack.push(i);
        }

        return answer;
    }
}
```

