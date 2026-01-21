# LeetCode-138 随机链表的复制（快速记忆）

## 题干
给你一个链表的头节点 `head`，每个节点除了 `next` 指针，还有一个 `random` 指针：
- `random` 可能指向链表中的任意节点，也可能是 `null`
请你返回这个链表的**深拷贝**（新链表的所有节点都必须是新创建的）。

## 数据范围（记忆版）
- 节点数：0 ~ 1000
- `Node.val`：`[-10^4, 10^4]`
- `random` 可以为 null 或指向任意节点

## 数据示例
- head = [[7,null],[13,0],[11,4],[10,2],[1,0]] → 返回深拷贝链表
- head = [] → []

## Java 函数入参/出参框架
```java
class Node {
    int val;
    Node next;
    Node random;
    Node(int val) { this.val = val; }
}

class Solution {
    public Node copyRandomList(Node head) {
        return null;
    }
}
```

## 最优解（无注释）
```java
class Node {
    int val;
    Node next;
    Node random;
    Node(int val) { this.val = val; }
}

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        Node cur = head;
        while (cur != null) {
            Node copy = new Node(cur.val);
            copy.next = cur.next;
            cur.next = copy;
            cur = copy.next;
        }

        cur = head;
        while (cur != null) {
            if (cur.random != null) {
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }

        Node dummy = new Node(0);
        Node tail = dummy;
        cur = head;
        while (cur != null) {
            Node copy = cur.next;
            Node next = copy.next;
            tail.next = copy;
            tail = copy;
            cur.next = next;
            cur = next;
        }

        return dummy.next;
    }
}
```

## 最优解（有注释）
```java
class Node {
    int val;
    Node next;
    Node random;
    Node(int val) { this.val = val; }
}

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        // 1) 把复制节点插到原节点后面：A -> A' -> B -> B' -> ...
        Node cur = head;
        while (cur != null) {
            Node copy = new Node(cur.val);
            copy.next = cur.next;
            cur.next = copy;
            cur = copy.next;
        }

        // 2) 处理 random：原节点的 random 指向谁，复制节点的 random 就指向“那个人的复制节点”
        cur = head;
        while (cur != null) {
            if (cur.random != null) {
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }

        // 3) 拆分：把交错的链表拆成“原链表”和“新链表”
        Node dummy = new Node(0);
        Node tail = dummy;
        cur = head;
        while (cur != null) {
            Node copy = cur.next;
            Node next = copy.next;

            tail.next = copy;
            tail = copy;

            cur.next = next; // 还原原链表
            cur = next;
        }

        return dummy.next;
    }
}
```

