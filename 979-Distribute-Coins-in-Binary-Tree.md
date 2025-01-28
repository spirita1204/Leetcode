# 979. Distribute Coins in Binary Tree

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

You are given the `root` of a binary tree with `n` nodes where each `node` in the tree has `node.val` coins. There are `n` coins in total throughout the whole tree.

In one move, we may choose two adjacent nodes and move one coin from one node to another. A move may be from parent to child, or from child to parent.

Return *the **minimum** number of moves required to make every node have **exactly** one coin*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/01/18/tree1.png](https://assets.leetcode.com/uploads/2019/01/18/tree1.png)

```
Input: root = [3,0,0]
Output: 2
Explanation:From the root of the tree, we move one coin to its left child, and one coin to its right child.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/01/18/tree2.png](https://assets.leetcode.com/uploads/2019/01/18/tree2.png)

```
Input: root = [0,3,0]
Output: 3
Explanation:From the left child of the root, we move two coins to the root [taking two moves]. Then, we move one coin from the root of the tree to the right child.

```

**Constraints:**

- The number of nodes in the tree is `n`.
- `1 <= n <= 100`
- `0 <= Node.val <= n`
- The sum of all `Node.val` is `n`.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 * int val;
 * TreeNode left;
 * TreeNode right;
 * TreeNode() {}
 * TreeNode(int val) { this.val = val; }
 * TreeNode(int val, TreeNode left, TreeNode right) {
 * this.val = val;
 * this.left = left;
 * this.right = right;
 * }
 * }
 */
class Solution {
    int ans = 0;

    public int distributeCoins(TreeNode root) {
        // 用邊去思考 計算每邊的流量
        balance(root);

        return ans;
    }

    private int balance(TreeNode root) {
        if (root == null)
            return 0;
        int leftFlow = balance(root.left);
        int rightFlow = balance(root.right);

        ans += Math.abs(leftFlow) + Math.abs(rightFlow);

        return leftFlow + rightFlow + (root.val - 1);
    }
}
```