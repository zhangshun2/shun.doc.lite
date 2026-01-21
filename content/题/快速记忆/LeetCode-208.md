# LeetCode-208 实现 Trie (前缀树)（快速记忆）

## 题干
请你实现一个 Trie（前缀树），支持：
- `insert(word)`：插入单词
- `search(word)`：查找单词是否存在
- `startsWith(prefix)`：查找是否存在以 prefix 为前缀的单词

## 数据范围（记忆版）
- 操作次数：最多约 `3 * 10^4`
- `word/prefix` 只包含小写英文字母
- `word/prefix` 长度：最多约 `2000`

## 数据示例
- insert("apple")
- search("apple") → true
- search("app") → false
- startsWith("app") → true
- insert("app")
- search("app") → true

## Java 函数入参/出参框架
```java
class Trie {
    public Trie() {
    }

    public void insert(String word) {
    }

    public boolean search(String word) {
        return false;
    }

    public boolean startsWith(String prefix) {
        return false;
    }
}
```

## 最优解（无注释）
```java
class Trie {
    private static class Node {
        Node[] next = new Node[26];
        boolean end;
    }

    private final Node root;

    public Trie() {
        this.root = new Node();
    }

    public void insert(String word) {
        Node cur = root;
        for (int i = 0; i < word.length(); i++) {
            int idx = word.charAt(i) - 'a';
            if (cur.next[idx] == null) {
                cur.next[idx] = new Node();
            }
            cur = cur.next[idx];
        }
        cur.end = true;
    }

    public boolean search(String word) {
        Node node = walk(word);
        return node != null && node.end;
    }

    public boolean startsWith(String prefix) {
        return walk(prefix) != null;
    }

    private Node walk(String s) {
        Node cur = root;
        for (int i = 0; i < s.length(); i++) {
            int idx = s.charAt(i) - 'a';
            if (cur.next[idx] == null) {
                return null;
            }
            cur = cur.next[idx];
        }
        return cur;
    }
}
```

## 最优解（有注释）
```java
class Trie {
    private static class Node {
        Node[] next = new Node[26]; // 只考虑小写字母
        boolean end;                // 是否是一个单词的结尾
    }

    private final Node root;

    public Trie() {
        this.root = new Node();
    }

    public void insert(String word) {
        Node cur = root;
        for (int i = 0; i < word.length(); i++) {
            int idx = word.charAt(i) - 'a';
            if (cur.next[idx] == null) {
                cur.next[idx] = new Node();
            }
            cur = cur.next[idx];
        }
        cur.end = true;
    }

    public boolean search(String word) {
        Node node = walk(word);
        return node != null && node.end;
    }

    public boolean startsWith(String prefix) {
        return walk(prefix) != null;
    }

    private Node walk(String s) {
        Node cur = root;
        for (int i = 0; i < s.length(); i++) {
            int idx = s.charAt(i) - 'a';
            if (cur.next[idx] == null) {
                return null;
            }
            cur = cur.next[idx];
        }
        return cur;
    }
}
```

