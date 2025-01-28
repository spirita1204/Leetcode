# 701. Insert into a Binary Search Tree

Methods: DFS
Difficulty: Medium

**Medium**

4.7K

158

Companies

You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree. Return *the root node of the BST after the insertion*. It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg](https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg)

```
Input: root = [4,2,7,1,3], val = 5
Output: [4,2,7,1,3,5]
Explanation: Another accepted tree is:

```

![https://assets.leetcode.com/uploads/2020/10/05/bst.jpg](https://assets.leetcode.com/uploads/2020/10/05/bst.jpg)

**Example 2:**

```
Input: root = [40,20,60,10,30,50,70], val = 25
Output: [40,20,60,10,30,50,70,null,null,25]

```

**Example 3:**

```
Input: root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
Output: [4,2,7,1,3,5]

```

**Constraints:**

- The number of nodes in the tree will be in the range `[0, 104]`.
- `108 <= Node.val <= 108`
- All the values `Node.val` are **unique**.
- `108 <= val <= 108`
- It's **guaranteed** that `val` does not exist in the original BST.

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root == null) return new TreeNode(val);
        dfs(root, val);
        return root;
    }
    public int dfs(TreeNode root, int val){
        if(root == null) return -1;//找到屬於位置

        if(val < root.val) {
            int l = dfs(root.left, val);
            if(l == -1) root.left = new TreeNode(val);
        }
        if(val > root.val){
            int r = dfs(root.right, val);
            if(r == -1) root.right = new TreeNode(val);
        }
        return 0;
    }
}
```