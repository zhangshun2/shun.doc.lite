# LeetCode-114 二叉树展开为链表（快速记忆）

## 题干
给你二叉树的根节点 `root`，请你把它展开为一个“单链表”：
- 这个单链表应该使用 `TreeNode.right` 指针作为 next
- `TreeNode.left` 全部置为 `null`
- 展开后的顺序与二叉树的**前序遍历**顺序相同
要求**原地修改**（不要求返回值）。

## 数据范围（记忆版）
- 节点数：0 ~ 2000
- 节点值范围：-100 ~ 100

## 数据示例
- root = [1,2,5,3,4,null,6] → [1,null,2,null,3,null,4,null,5,null,6]
- root = [] → []
- root = [0] → [0]

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
    public void flatten(TreeNode root) {
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
    public void flatten(TreeNode root) {
        TreeNode cur = root;
        while (cur != null) {
            if (cur.left != null) {
                TreeNode rightMost = cur.left;
                while (rightMost.right != null) {
                    rightMost = rightMost.right;
                }
                rightMost.right = cur.right;
                cur.right = cur.left;
                cur.left = null;
            }
            cur = cur.right;
        }
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
    public void flatten(TreeNode root) {
        TreeNode cur = root;

        // 从上到下处理，每次把“左子树”搬到“右边”，并把原来的右子树接到左子树最右边
        while (cur != null) {
            if (cur.left != null) {
                TreeNode rightMost = cur.left;
                while (rightMost.right != null) {
                    rightMost = rightMost.right;
                }

                rightMost.right = cur.right;
                cur.right = cur.left;
                cur.left = null;
            }

            cur = cur.right;
        }
    }
}
```

