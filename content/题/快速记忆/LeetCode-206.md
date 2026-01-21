# LeetCode-206 反转链表（快速记忆）

## 题干
给你单链表的头节点 `head`，请你反转链表，并返回反转后的头节点。

## 数据范围（记忆版）
- 节点数：0 ~ 5000
- 节点值范围：-5000 ~ 5000

## 数据示例
- head = [1,2,3,4,5] → [5,4,3,2,1]
- head = [1,2] → [2,1]
- head = [] → []

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
    public ListNode reverseList(ListNode head) {
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
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode next = cur.next;
            cur.next = prev;
            prev = cur;
            cur = next;
        }
        return prev;
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
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;

        while (cur != null) {
            ListNode next = cur.next; // 先保存下一节点，否则链会断
            cur.next = prev;          // 反转指针
            prev = cur;               // prev 和 cur 同步向前
            cur = next;
        }

        return prev; // prev 最后停在新头节点
    }
}
```

