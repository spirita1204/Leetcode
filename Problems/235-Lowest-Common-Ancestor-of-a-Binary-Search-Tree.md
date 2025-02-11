# 235. Lowest Common Ancestor of a Binary Search Tree

Methods: Basic logic
Difficulty: Medium

**Medium**

9.2K

258

Companies

Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

```

**Example 3:**

```
Input: root = [2,1], p = 2, q = 1
Output: 2

```

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the BST.

```jsx
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    /* my solution
    TreeNode res;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        dfs(root, p, q);
        if(res == null) inLine(root, p, q); 
        return res;
    }
    public boolean dfs(TreeNode root, TreeNode p, TreeNode q){// DFS判斷左右是否有
        if(root == null) return false; 
        if(root == p || root == q) return true;
        boolean left = dfs(root.left, p, q);
        boolean right = dfs(root.right, p, q);

        if(left && right) res = root;
        return left || right;
    }
    public void inLine(TreeNode root, TreeNode p, TreeNode q){// BFS判斷同一線上是否有
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()){
            TreeNode sub = queue.poll();
            if(sub == p || sub == q){
                res = sub;
                break;
            }
            if(sub.left != null) queue.offer(sub.left);
            if(sub.right != null) queue.offer(sub.right);
        }
    }
    */
    /** best */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
        else if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
        else return root;
    }
}
```