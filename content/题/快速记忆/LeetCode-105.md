# LeetCode-105 从前序与中序遍历序列构造二叉树（快速记忆）

## 题干
给你两个整数数组 `preorder` 和 `inorder`，它们分别是同一棵二叉树的前序遍历和中序遍历。
请你构造这棵二叉树并返回其根节点。

## 数据范围（记忆版）
- `1 <= preorder.length == inorder.length <= 3000`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` 和 `inorder` 都由**不重复**的值组成

## 数据示例
- preorder = [3,9,20,15,7], inorder = [9,3,15,20,7] → [3,9,20,null,null,15,7]
- preorder = [-1], inorder = [-1] → [-1]

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> pos = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            pos.put(inorder[i], i);
        }
        return dfs(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, pos);
    }

    private TreeNode dfs(int[] preorder, int pl, int pr, int[] inorder, int il, int ir, Map<Integer, Integer> pos) {
        if (pl > pr) {
            return null;
        }
        int rootVal = preorder[pl];
        int k = pos.get(rootVal);
        int leftSize = k - il;
        TreeNode root = new TreeNode(rootVal);
        root.left = dfs(preorder, pl + 1, pl + leftSize, inorder, il, k - 1, pos);
        root.right = dfs(preorder, pl + leftSize + 1, pr, inorder, k + 1, ir, pos);
        return root;
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // inorder 里每个值的位置，方便 O(1) 找到根在哪
        Map<Integer, Integer> pos = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            pos.put(inorder[i], i);
        }

        return dfs(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, pos);
    }

    // preorder[pl..pr] 和 inorder[il..ir] 表示同一棵子树
    private TreeNode dfs(int[] preorder, int pl, int pr, int[] inorder, int il, int ir, Map<Integer, Integer> pos) {
        if (pl > pr) {
            return null;
        }

        // 前序遍历：第一个就是根
        int rootVal = preorder[pl];

        // 根在中序里的位置，把中序分成左子树和右子树
        int k = pos.get(rootVal);
        int leftSize = k - il;

        TreeNode root = new TreeNode(rootVal);

        // 左子树：前序紧跟着根的 leftSize 个元素
        root.left = dfs(preorder, pl + 1, pl + leftSize, inorder, il, k - 1, pos);

        // 右子树：剩下的部分
        root.right = dfs(preorder, pl + leftSize + 1, pr, inorder, k + 1, ir, pos);

        return root;
    }
}
```

