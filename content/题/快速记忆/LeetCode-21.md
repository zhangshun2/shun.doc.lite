# LeetCode-21 合并两个有序链表（快速记忆）

## 题干
给你两个**升序**链表 `list1` 和 `list2`，把它们合并成一个**升序**链表，并返回合并后的链表头节点。

## 数据范围（记忆版）
- 两个链表的节点数：0 ~ 50
- 节点值范围：-100 ~ 100
- 两个链表都已经是升序（非递减）排列

## 数据示例
- list1 = [1,2,4], list2 = [1,3,4] → [1,1,2,3,4,4]
- list1 = [], list2 = [] → []
- list1 = [], list2 = [0] → [0]

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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                tail.next = list1;
                list1 = list1.next;
            } else {
                tail.next = list2;
                list2 = list2.next;
            }
            tail = tail.next;
        }

        tail.next = (list1 != null) ? list1 : list2;
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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(0); // 哑节点：让“结果链表的头”处理更统一
        ListNode tail = dummy;            // tail 永远指向结果链表的最后一个节点

        while (list1 != null && list2 != null) {
            // 每次把更小的那个节点接到 tail 后面
            if (list1.val <= list2.val) {
                tail.next = list1;
                list1 = list1.next;
            } else {
                tail.next = list2;
                list2 = list2.next;
            }
            tail = tail.next; // tail 往后走一步
        }

        // 其中一条链走完了，另一条链剩下的部分直接接上即可
        tail.next = (list1 != null) ? list1 : list2;
        return dummy.next;
    }
}
```
