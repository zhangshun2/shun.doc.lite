# LeetCode-25 K 个一组翻转链表（快速记忆）

## 题干
给你一个链表头节点 `head` 和一个整数 `k`，请你每 `k` 个节点为一组进行翻转，并返回翻转后的链表。

如果最后剩下的节点数不足 `k` 个，就保持原来的顺序，不翻转。

## 数据范围（记忆版）
- 节点数：1 ~ 5000
- 1 <= k <= 节点数
- 节点值范围：0 ~ 1000

## 数据示例
- head = [1,2,3,4,5], k = 2 → [2,1,4,3,5]
- head = [1,2,3,4,5], k = 3 → [3,2,1,4,5]

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
    public ListNode reverseKGroup(ListNode head, int k) {
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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0, head);
        ListNode groupPrev = dummy;

        while (true) {
            ListNode kth = getKth(groupPrev, k);
            if (kth == null) {
                break;
            }

            ListNode groupNext = kth.next;
            ListNode prev = groupNext;
            ListNode cur = groupPrev.next;

            while (cur != groupNext) {
                ListNode next = cur.next;
                cur.next = prev;
                prev = cur;
                cur = next;
            }

            ListNode newGroupHead = kth;
            ListNode newGroupTail = groupPrev.next;
            groupPrev.next = newGroupHead;
            groupPrev = newGroupTail;
        }

        return dummy.next;
    }

    private ListNode getKth(ListNode start, int k) {
        ListNode cur = start;
        for (int i = 0; i < k; i++) {
            if (cur.next == null) {
                return null;
            }
            cur = cur.next;
        }
        return cur;
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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0, head); // 哑节点，方便处理头节点被翻转的情况
        ListNode groupPrev = dummy;             // groupPrev 指向“当前这一组”的前一个节点

        while (true) {
            // 先找到当前组的第 k 个节点：找不到说明不足 k 个，不能翻
            ListNode kth = getKth(groupPrev, k);
            if (kth == null) {
                break;
            }

            // groupNext 是这一组后面的第一个节点（下一组的开头）
            ListNode groupNext = kth.next;

            // 下面开始翻转 groupPrev.next 到 kth 这一段
            // prev 初始指向 groupNext，这样翻转后尾巴能直接连上 groupNext
            ListNode prev = groupNext;
            ListNode cur = groupPrev.next;
            while (cur != groupNext) {
                ListNode next = cur.next;
                cur.next = prev;
                prev = cur;
                cur = next;
            }

            // 翻转完成后：
            // kth 变成新组头
            // groupPrev.next（旧组头）变成新组尾
            ListNode newGroupHead = kth;
            ListNode newGroupTail = groupPrev.next;
            groupPrev.next = newGroupHead;
            groupPrev = newGroupTail;
        }

        return dummy.next;
    }

    private ListNode getKth(ListNode start, int k) {
        ListNode cur = start;
        for (int i = 0; i < k; i++) {
            if (cur.next == null) {
                return null;
            }
            cur = cur.next;
        }
        return cur;
    }
}
```
