# LeetCode-199 二叉树的右视图（快速记忆）

## 题干
给你一棵二叉树的根节点 `root`，想象你站在树的右侧，返回从上到下看到的节点值。

## 数据范围（记忆版）
- 节点数：0 ~ 100
- 节点值范围：-100 ~ 100

## 数据示例
- root = [1,2,3,null,5,null,4] → [1,3,4]
- root = [1,null,3] → [1,3]
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
    public List<Integer> rightSideView(TreeNode root) {
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Deque<TreeNode> q = new ArrayDeque<>();
        q.addLast(root);
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.removeFirst();
                if (i == size - 1) {
                    ans.add(node.val);
                }
                if (node.left != null) q.addLast(node.left);
                if (node.right != null) q.addLast(node.right);
            }
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }

        Deque<TreeNode> q = new ArrayDeque<>();
        q.addLast(root);

        // 层序遍历：每层最后一个节点，就是从右边看到的那个
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.removeFirst();

                if (i == size - 1) {
                    ans.add(node.val);
                }

                if (node.left != null) q.addLast(node.left);
                if (node.right != null) q.addLast(node.right);
            }
        }

        return ans;
    }
}
```

