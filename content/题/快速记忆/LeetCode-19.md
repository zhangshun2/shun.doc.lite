# LeetCode-19 删除链表的倒数第 N 个结点（快速记忆）

## 题干
给你一个链表头节点 `head` 和整数 `n`，请删除链表的倒数第 `n` 个节点，并返回头节点。

## 数据范围（记忆版）
- 典型双指针：fast 先走 n 步，再一起走
- 删除头节点的情况需要处理

## 数据示例
- head = [1,2,3,4,5], n = 2 → [1,2,3,5]
- head = [1], n = 1 → []

## Java 函数入参/出参框架
```java
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        return null;
    }
}
```

## 最优解（无注释）
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        ListNode fast = dummy;
        ListNode slow = dummy;

        for (int i = 0; i < n; i++) fast = fast.next;
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

## 最优解（有注释）
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);

        ListNode fast = dummy;
        ListNode slow = dummy;

        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }

        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

