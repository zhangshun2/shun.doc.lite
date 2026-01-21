# LeetCode-98 验证二叉搜索树（快速记忆）

## 题干
给你一个二叉树的根节点 `root`，判断它是不是一棵**有效的二叉搜索树（BST）**。
BST 条件：对任意节点，左子树所有节点值 < 它，右子树所有节点值 > 它；并且左右子树也都满足 BST。

## 数据范围（记忆版）
- 节点数：1 ~ 10^4
- 节点值范围：`[-2^31, 2^31 - 1]`

## 数据示例
- root = [2,1,3] → true
- root = [5,1,4,null,null,3,6] → false

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
    public boolean isValidBST(TreeNode root) {
        return false;
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
    public boolean isValidBST(TreeNode root) {
        return dfs(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean dfs(TreeNode node, long low, long high) {
        if (node == null) {
            return true;
        }
        if (node.val <= low || node.val >= high) {
            return false;
        }
        return dfs(node.left, low, node.val) && dfs(node.right, node.val, high);
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
    public boolean isValidBST(TreeNode root) {
        // 用“上下界”约束每个节点允许的取值范围
        return dfs(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean dfs(TreeNode node, long low, long high) {
        if (node == null) {
            return true;
        }

        // 注意是严格小于/严格大于（BST 不允许相等）
        if (node.val <= low || node.val >= high) {
            return false;
        }

        // 左子树：上界变成当前节点值
        // 右子树：下界变成当前节点值
        return dfs(node.left, low, node.val) && dfs(node.right, node.val, high);
    }
}
```

