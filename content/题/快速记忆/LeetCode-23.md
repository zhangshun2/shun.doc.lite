# LeetCode-23 合并 K 个升序链表（快速记忆）

## 题干
给你一个链表数组 `lists`，每个链表都已经按升序排列。请你把它们合并成一个升序链表，并返回合并后的链表头节点。

## 数据范围（记忆版）
- lists.length：0 ~ 10^4
- 所有链表节点总数：0 ~ 10^4
- 节点值范围：-10^4 ~ 10^4
- 每个链表都是升序（非递减）

## 数据示例
- lists = [[1,4,5],[1,3,4],[2,6]] → [1,1,2,3,4,4,5,6]
- lists = [] → []
- lists = [[]] → []

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
    public ListNode mergeKLists(ListNode[] lists) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.PriorityQueue;

public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a.val, b.val));
        for (ListNode head : lists) {
            if (head != null) {
                minHeap.offer(head);
            }
        }

        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (!minHeap.isEmpty()) {
            ListNode node = minHeap.poll();
            tail.next = node;
            tail = tail.next;
            if (node.next != null) {
                minHeap.offer(node.next);
            }
        }

        tail.next = null;
        return dummy.next;
    }
}
```

## 最优解（有注释）
```java
import java.util.PriorityQueue;

public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        // 最小堆：堆顶永远是当前所有链表头节点中的最小值
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a.val, b.val));

        for (ListNode head : lists) {
            if (head != null) {
                minHeap.offer(head);
            }
        }

        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (!minHeap.isEmpty()) {
            // 每次取出一个最小节点，把它接到结果链表后面
            ListNode node = minHeap.poll();
            tail.next = node;
            tail = tail.next;

            // 这个节点来自某一条链表，把它的下一个节点继续放进堆
            if (node.next != null) {
                minHeap.offer(node.next);
            }
        }

        tail.next = null;
        return dummy.next;
    }
}
```
