# 872. Leaf-Similar Trees

Methods: DFS
Difficulty: Easy

Easy

Topics

Companies

Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a **leaf value sequence***.*

![https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/16/tree.png](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/16/tree.png)

For example, in the given tree above, the leaf value sequence is `(6, 7, 4, 9, 8)`.

Two binary trees are considered *leaf-similar* if their leaf value sequence is the same.

Return `true` if and only if the two given trees with head nodes `root1` and `root2` are leaf-similar.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-1.jpg](https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-1.jpg)

```
Input: root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-2.jpg](https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-2.jpg)

```
Input: root1 = [1,2,3], root2 = [1,3,2]
Output: false

```

**Constraints:**

- The number of nodes in each tree will be in the range `[1, 200]`.
- Both of the given trees will have values in the range `[0, 200]`.

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
    List<Integer> list = new ArrayList<>();
    List<Integer> list2 = new ArrayList<>();

    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        dfs1(root1);
        dfs2(root2);
        if(list.size() != list2.size()) return false;
        for(int i = 0; i < list.size(); i++) {
            if(list.get(i) != list2.get(i)) return false;
        }
        return true;
    }
    private TreeNode dfs1(TreeNode root1) {
        if(root1 == null) {
            return null;
        }
        TreeNode left = dfs1(root1.left);
        TreeNode right = dfs1(root1.right);

        if(left == null && right == null) 
            list.add(root1.val);

        return root1;
    }

    private TreeNode dfs2(TreeNode root2) {
        if(root2 == null) {
            return null;
        }
        TreeNode left = dfs2(root2.left);
        TreeNode right = dfs2(root2.right);

        if(left == null && right == null) 
            list2.add(root2.val);

        return root2;
    }
}
```