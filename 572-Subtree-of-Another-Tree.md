# 572. Subtree of Another Tree

Methods: BFS
Difficulty: Easy

**Easy**

7.1K

404

Companies

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false

```

**Constraints:**

- The number of nodes in the `root` tree is in the range `[1, 2000]`.
- The number of nodes in the `subRoot` tree is in the range `[1, 1000]`.
- `104 <= root.val <= 104`
- `104 <= subRoot.val <= 104`

```jsx
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
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {//bfs 走訪每個點
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while(!q.isEmpty()){
            TreeNode node = q.poll();

            if(node.val == subRoot.val){
                //依樣的話回傳 true
                if(isSame(node, subRoot)) return true;
            }
            if(node.left != null) q.offer(node.left);
            if(node.right != null) q.offer(node.right);
        }
        return false;
    }
    public boolean isSame(TreeNode node, TreeNode subRoot){// dfs 判斷兩樹是否一致
        if(node == null && subRoot != null) return false;
        else if(node != null && subRoot == null) return false;
        
        if(node == null || subRoot == null) return true;
        else if(node.val != subRoot.val) return false;//當兩值不同 回傳false

        boolean left = isSame(node.left, subRoot.left);
        boolean right = isSame(node.right, subRoot.right);

        return (left && right);
    }
}
```