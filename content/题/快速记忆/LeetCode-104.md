# LeetCode-104 二叉树的最大深度（快速记忆）

## 题干
给你一棵二叉树的根节点 `root`，返回它的最大深度。
最大深度：从根节点到最远叶子节点的最长路径上的节点数。

## 数据范围（记忆版）
- 节点数：0 ~ 10^4
- 节点值范围：-100 ~ 100

## 数据示例
- root = [3,9,20,null,null,15,7] → 3
- root = [1,null,2] → 2
- root = [] → 0

## Java 函数入参/出参框架
```java
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
    public int maxDepth(TreeNode root) {
        return 0;
    }
}
```

## 最优解（无注释）
```java
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
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

## 最优解（有注释）
```java
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
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        // 当前节点的最大深度 = 1（自己） + 左右子树最大深度的较大者
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return 1 + Math.max(left, right);
    }
}
```

