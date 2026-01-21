# LeetCode-124 二叉树中的最大路径和（快速记忆）

## 题干
二叉树中的路径定义为：从任意节点出发，沿父子连接走到任意节点，路径中至少包含一个节点。
路径不一定经过根节点。
返回这棵树的最大路径和。

## 数据范围（记忆版）
- 节点数：1 ~ 3 * 10^4
- 节点值范围：-1000 ~ 1000

## 数据示例
- root = [1,2,3] → 6
- root = [-10,9,20,null,null,15,7] → 42

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
    public int maxPathSum(TreeNode root) {
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
    public int maxPathSum(TreeNode root) {
        int[] ans = new int[] { Integer.MIN_VALUE };
        dfs(root, ans);
        return ans[0];
    }

    private int dfs(TreeNode node, int[] ans) {
        if (node == null) {
            return 0;
        }
        int left = Math.max(0, dfs(node.left, ans));
        int right = Math.max(0, dfs(node.right, ans));
        ans[0] = Math.max(ans[0], node.val + left + right);
        return node.val + Math.max(left, right);
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
    public int maxPathSum(TreeNode root) {
        int[] ans = new int[] { Integer.MIN_VALUE };
        dfs(root, ans);
        return ans[0];
    }

    // 返回：从 node 出发，向下走（只能选一边）的最大路径和
    private int dfs(TreeNode node, int[] ans) {
        if (node == null) {
            return 0;
        }

        // 如果子树贡献为负，宁愿不选它（当作 0）
        int leftGain = Math.max(0, dfs(node.left, ans));
        int rightGain = Math.max(0, dfs(node.right, ans));

        // 以 node 为“拐点”的路径：左 + node + 右
        ans[0] = Math.max(ans[0], node.val + leftGain + rightGain);

        // 向父节点汇报时，只能选一边继续向上延伸
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

