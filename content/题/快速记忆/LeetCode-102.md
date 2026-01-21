# LeetCode-102 二叉树的层序遍历（快速记忆）

## 题干
给你二叉树的根节点 `root`，返回其节点值的**层序遍历**（按层从左到右）。

## 数据范围（记忆版）
- 节点数：0 ~ 2000
- 节点值范围：-1000 ~ 1000

## 数据示例
- root = [3,9,20,null,null,15,7] → [[3],[9,20],[15,7]]
- root = [1] → [[1]]
- root = [] → []

## Java 函数入参/出参框架
```java
import java.util.*;

public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        return null;
    }
}
```

## 最优解（无注释）
```java
import java.util.*;

public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Deque<TreeNode> q = new ArrayDeque<>();
        q.addLast(root);
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>(size);
            for (int i = 0; i < size; i++) {
                TreeNode node = q.removeFirst();
                level.add(node.val);
                if (node.left != null) q.addLast(node.left);
                if (node.right != null) q.addLast(node.right);
            }
            ans.add(level);
        }
        return ans;
    }
}
```

## 最优解（有注释）
```java
import java.util.*;

public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }

        Deque<TreeNode> q = new ArrayDeque<>();
        q.addLast(root);

        while (!q.isEmpty()) {
            int size = q.size(); // 当前层的节点数量
            List<Integer> level = new ArrayList<>(size);

            for (int i = 0; i < size; i++) {
                TreeNode node = q.removeFirst();
                level.add(node.val);

                if (node.left != null) q.addLast(node.left);
                if (node.right != null) q.addLast(node.right);
            }

            ans.add(level);
        }

        return ans;
    }
}
```

