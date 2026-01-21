# LeetCode-155 最小栈（快速记忆）

## 题干
请你设计一个栈，除了支持 `push`、`pop`、`top` 外，还要支持 `getMin`，并且这些操作都要是 **O(1)**。

`getMin` 返回当前栈里的最小元素。

## 数据范围（记忆版）
- 调用次数最多 30000 次
- 入栈整数范围：-2^31 ~ 2^31 - 1

## 数据示例
- push(-2), push(0), push(-3), getMin() → -3
- pop(), top() → 0, getMin() → -2

## Java 函数入参/出参框架
```java
class MinStack {
    public MinStack() {
    }

    public void push(int val) {
    }

    public void pop() {
    }

    public int top() {
        return 0;
    }

    public int getMin() {
        return 0;
    }
}
```

## 最优解（无注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class MinStack {
    private final Deque<Integer> stack = new ArrayDeque<>();
    private final Deque<Integer> minStack = new ArrayDeque<>();

    public MinStack() {
    }

    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        int top = stack.pop();
        if (top == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

## 最优解（有注释）
```java
import java.util.ArrayDeque;
import java.util.Deque;

class MinStack {
    // stack：正常的数据栈
    private final Deque<Integer> stack = new ArrayDeque<>();

    // minStack：辅助栈，栈顶永远是“当前最小值”
    private final Deque<Integer> minStack = new ArrayDeque<>();

    public MinStack() {
    }

    public void push(int val) {
        stack.push(val);

        // 当 val <= 当前最小值时，把它也压入 minStack
        // 这样处理“最小值重复出现”的情况也不会出错
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        int top = stack.pop();

        // 如果弹出的就是最小值，也要把 minStack 的栈顶同步弹出
        if (top == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

