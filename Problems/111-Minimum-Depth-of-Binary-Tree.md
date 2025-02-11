# 111. Minimum Depth of Binary Tree

Methods: DFS
Difficulty: Easy

Easy

Topics

Companies

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note:** A leaf is a node with no children.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 2

```

**Example 2:**

```
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 105]`.
- `1000 <= Node.val <= 1000`

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
    public int minDepth(TreeNode root) {
        if (root == null)
            return 0;
        int left = minDepth(root.left);
        int right = minDepth(root.right);

        if (left == 0 && right != 0) return right + 1;
        if (left != 0 && right == 0) return left + 1;
        
        return Math.min(left, right) + 1;
    }
}
```