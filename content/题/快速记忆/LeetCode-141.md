# LeetCode-141 环形链表（快速记忆）

## 题干
给你一个链表的头节点 `head`，判断链表中是否有环。
如果链表中存在某个节点可以通过连续跟随 `next` 指针再次到达，则链表有环。

## 数据范围（记忆版）
- 节点数：0 ~ 10^4
- 节点值范围：`[-10^5, 10^5]`

## 数据示例
- head = [3,2,0,-4], pos = 1 → true
- head = [1,2], pos = 0 → true
- head = [1], pos = -1 → false

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
    public boolean hasCycle(ListNode head) {
        return false;
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
    public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
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
    public boolean hasCycle(ListNode head) {
        ListNode slow = head; // 一次走 1 步
        ListNode fast = head; // 一次走 2 步

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            // 有环的话，快慢指针一定会在环内相遇
            if (slow == fast) {
                return true;
            }
        }

        return false;
    }
}
```

