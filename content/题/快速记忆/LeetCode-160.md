# LeetCode-160 相交链表（快速记忆）

## 题干
给你两个单链表的头节点 `headA` 和 `headB`，返回两个链表相交的起始节点。
如果两个链表不相交，返回 `null`。

## 数据范围（记忆版）
- 两个链表节点数：0 ~ 3 * 10^4
- 节点值范围：`[-10^5, 10^5]`

## 数据示例
- A = [4,1,8,4,5], B = [5,6,1,8,4,5] → 相交起点值为 8 的节点
- A = [1,9,1,2,4], B = [3,2,4] → 相交起点值为 2 的节点
- A = [2,6,4], B = [1,5] → null

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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode a = headA;
        ListNode b = headB;
        while (a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;
        }
        return a;
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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode a = headA;
        ListNode b = headB;

        // a 走完 A 就去走 B；b 走完 B 就去走 A
        // 如果有相交，两者会在相交点相遇；如果不相交，两者会同时走到 null
        while (a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;
        }

        return a;
    }
}
```

