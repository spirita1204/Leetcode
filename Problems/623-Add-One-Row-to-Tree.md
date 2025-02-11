# 623. Add One Row to Tree

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Given the `root` of a binary tree and two integers `val` and `depth`, add a row of nodes with value `val` at the given depth `depth`.

Note that the `root` node is at depth `1`.

The adding rule is:

- Given the integer `depth`, for each not null tree node `cur` at the depth `depth - 1`, create two tree nodes with value `val` as `cur`'s left subtree root and right subtree root.
- `cur`'s original left subtree should be the left subtree of the new left subtree root.
- `cur`'s original right subtree should be the right subtree of the new right subtree root.
- If `depth == 1` that means there is no depth `depth - 1` at all, then create a tree node with value `val` as the new root of the whole original tree, and the original tree is the new root's left subtree.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/03/15/addrow-tree.jpg](https://assets.leetcode.com/uploads/2021/03/15/addrow-tree.jpg)

```
Input: root = [4,2,6,3,1,5], val = 1, depth = 2
Output: [4,1,1,2,null,null,6,3,1,5]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/03/11/add2-tree.jpg](https://assets.leetcode.com/uploads/2021/03/11/add2-tree.jpg)

```
Input: root = [4,2,null,3,1], val = 1, depth = 3
Output: [4,2,null,1,1,3,null,null,1]

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- The depth of the tree is in the range `[1, 104]`.
- `100 <= Node.val <= 100`
- `105 <= val <= 105`
- `1 <= depth <= the depth of tree + 1`

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode addOneRow(TreeNode root, int val, int depth) {
        return dfs(root, 0, depth, val, false);
    }
    // dir true代表右子樹false左
    private TreeNode dfs (TreeNode root, int depthNow, int depth, int val, boolean dir) {
        // 當插入節點為leaf
        if(root == null && depthNow == depth - 1) return new TreeNode(val);
        // 到leaf
        if(root == null) return null;
        // 加入節點
        if(depthNow == depth - 1) {
            TreeNode addedNode = new TreeNode(val);

            if(dir) addedNode.right = root;
            else addedNode.left = root;
  
            return addedNode;
        }
        root.left = dfs(root.left, depthNow + 1, depth, val, false);
        root.right = dfs(root.right, depthNow + 1, depth, val, true);

        return root;
    }
}
```