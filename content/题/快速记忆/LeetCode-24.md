# LeetCode-24 两两交换链表中的节点（快速记忆）

## 题干
给你一个链表的头节点 `head`，请你把链表中每两个相邻的节点交换一次，并返回交换后的链表。

你不能只是改变节点的值，必须实际交换节点本身。

## 数据范围（记忆版）
- 节点数：0 ~ 100
- 节点值范围：0 ~ 100

## 数据示例
- head = [1,2,3,4] → [2,1,4,3]
- head = [] → []
- head = [1] → [1]

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
    public ListNode swapPairs(ListNode head) {
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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0, head);
        ListNode prev = dummy;

        while (prev.next != null && prev.next.next != null) {
            ListNode first = prev.next;
            ListNode second = prev.next.next;

            first.next = second.next;
            second.next = first;
            prev.next = second;

            prev = first;
        }

        return dummy.next;
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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0, head); // 哑节点，统一处理头节点会被交换的情况
        ListNode prev = dummy;                  // prev 指向“每一对要交换的两个节点”之前的那个节点

        while (prev.next != null && prev.next.next != null) {
            ListNode first = prev.next;
            ListNode second = prev.next.next;

            // 交换前：prev -> first -> second -> ...
            // 交换后：prev -> second -> first -> ...
            first.next = second.next;
            second.next = first;
            prev.next = second;

            // prev 往后走两步，走到这一对交换后的尾巴（也就是 first）
            prev = first;
        }

        return dummy.next;
    }
}
```
