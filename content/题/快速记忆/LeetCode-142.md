# LeetCode-142 环形链表 II（快速记忆）

## 题干
给你一个链表的头节点 `head`，返回链表开始入环的第一个节点。
如果链表无环，返回 `null`。

## 数据范围（记忆版）
- 节点数：0 ~ 10^4
- 节点值范围：`[-10^5, 10^5]`

## 数据示例
- head = [3,2,0,-4], pos = 1 → 返回值为值 2 的节点
- head = [1,2], pos = 0 → 返回值为值 1 的节点
- head = [1], pos = -1 → null

## Java 函数入参/出参框架
```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode detectCycle(ListNode head) {
        return null;
    }
}
```

## 最优解（无注释）
```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                ListNode p1 = head;
                ListNode p2 = slow;
                while (p1 != p2) {
                    p1 = p1.next;
                    p2 = p2.next;
                }
                return p1;
            }
        }
        return null;
    }
}
```

## 最优解（有注释）
```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        // 先判断是否有环，并找到相遇点
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                // 有环：从头节点和相遇点同时出发，每次走一步，相遇点就是入环点
                ListNode p1 = head;
                ListNode p2 = slow;
                while (p1 != p2) {
                    p1 = p1.next;
                    p2 = p2.next;
                }
                return p1;
            }
        }

        return null;
    }
}
```

