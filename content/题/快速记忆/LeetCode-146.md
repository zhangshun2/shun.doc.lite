# LeetCode-146 LRU 缓存（快速记忆）

## 题干
请你设计并实现一个满足 **LRU（最近最少使用）** 缓存约束的数据结构。
实现 `LRUCache` 类：
- `LRUCache(int capacity)`：以正整数作为容量 `capacity` 初始化 LRU 缓存
- `int get(int key)`：如果 key 存在，返回 value，否则返回 -1
- `void put(int key, int value)`：如果 key 存在则更新 value；否则插入新 key-value。如果超过容量，要删除**最久未使用**的 key
要求 `get` 和 `put` 都是 `O(1)` 平均时间复杂度。

## 数据范围（记忆版）
- `1 <= capacity <= 3000`
- `0 <= key <= 10^4`
- `0 <= value <= 10^5`
- `get/put` 总调用次数：最多约 `2 * 10^5`

## 数据示例
- capacity = 2
- put(1,1), put(2,2), get(1)=1, put(3,3)（淘汰 2）, get(2)=-1, put(4,4)（淘汰 1）, get(1)=-1, get(3)=3, get(4)=4

## Java 函数入参/出参框架
```java
class LRUCache {
    public LRUCache(int capacity) {
    }

    public int get(int key) {
        return 0;
    }

    public void put(int key, int value) {
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

class LRUCache {
    private static class Node {
        int key;
        int val;
        Node prev;
        Node next;
        Node(int key, int val) { this.key = key; this.val = val; }
    }

    private final int capacity;
    private final Map<Integer, Node> map;
    private final Node head;
    private final Node tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        Node node = map.get(key);
        if (node == null) {
            return -1;
        }
        moveToFront(node);
        return node.val;
    }

    public void put(int key, int value) {
        Node node = map.get(key);
        if (node != null) {
            node.val = value;
            moveToFront(node);
            return;
        }

        if (map.size() == capacity) {
            Node lru = tail.prev;
            remove(lru);
            map.remove(lru.key);
        }

        Node fresh = new Node(key, value);
        addToFront(fresh);
        map.put(key, fresh);
    }

    private void moveToFront(Node node) {
        remove(node);
        addToFront(node);
    }

    private void addToFront(Node node) {
        Node a = head;
        Node b = head.next;
        node.prev = a;
        node.next = b;
        a.next = node;
        b.prev = node;
    }

    private void remove(Node node) {
        Node a = node.prev;
        Node b = node.next;
        a.next = b;
        b.prev = a;
        node.prev = null;
        node.next = null;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

class LRUCache {
    private static class Node {
        int key;
        int val;
        Node prev;
        Node next;
        Node(int key, int val) { this.key = key; this.val = val; }
    }

    private final int capacity;
    private final Map<Integer, Node> map; // key -> 节点，O(1) 找到节点
    private final Node head;              // 双向链表哑头
    private final Node tail;              // 双向链表哑尾

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();

        // 双向链表：头部是“最近使用”，尾部是“最久未使用”
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        Node node = map.get(key);
        if (node == null) {
            return -1;
        }

        // 被访问过，就变成“最近使用”
        moveToFront(node);
        return node.val;
    }

    public void put(int key, int value) {
        Node node = map.get(key);
        if (node != null) {
            node.val = value;
            moveToFront(node);
            return;
        }

        // 超容量：删掉最久未使用（尾部的前一个）
        if (map.size() == capacity) {
            Node lru = tail.prev;
            remove(lru);
            map.remove(lru.key);
        }

        Node fresh = new Node(key, value);
        addToFront(fresh);
        map.put(key, fresh);
    }

    private void moveToFront(Node node) {
        remove(node);
        addToFront(node);
    }

    private void addToFront(Node node) {
        Node a = head;
        Node b = head.next;
        node.prev = a;
        node.next = b;
        a.next = node;
        b.prev = node;
    }

    private void remove(Node node) {
        Node a = node.prev;
        Node b = node.next;
        a.next = b;
        b.prev = a;
        node.prev = null;
        node.next = null;
    }
}
```

