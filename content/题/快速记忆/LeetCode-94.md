# LeetCode-94 二叉树的中序遍历（快速记忆）

## 题干
给你一棵二叉树的根节点 `root`，返回它的**中序遍历**结果。
中序遍历顺序：左子树 → 根 → 右子树。

## 数据范围（记忆版）
- 节点数：0 ~ 100
- 节点值范围：-100 ~ 100

## 数据示例
- root = [1,null,2,3] → [1,3,2]
- root = [] → []
- root = [1] → [1]

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
    public List<Integer> inorderTraversal(TreeNode root) {
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Deque<TreeNode> st = new ArrayDeque<>();
        TreeNode cur = root;

        while (cur != null || !st.isEmpty()) {
            while (cur != null) {
                st.push(cur);
                cur = cur.left;
            }
            cur = st.pop();
            ans.add(cur.val);
            cur = cur.right;
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Deque<TreeNode> st = new ArrayDeque<>();
        TreeNode cur = root;

        // 核心：一路向左入栈，出栈访问，再转向右子树
        while (cur != null || !st.isEmpty()) {
            while (cur != null) {
                st.push(cur);
                cur = cur.left;
            }

            cur = st.pop();
            ans.add(cur.val);

            cur = cur.right;
        }

        return ans;
    }
}
```

