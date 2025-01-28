# 107. Binary Tree Level Order Traversal II

Methods: BFS
Difficulty: Medium

Given the `root` of a binary tree, return *the bottom-up level order traversal of its nodes' values*. (i.e., from left to right, level by level from leaf to root).

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]

```

**Example 2:**

```
Input: root = [1]
Output: [[1]]

```

**Example 3:**

```
Input: root = []
Output: []

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `1000 <= Node.val <= 1000`

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if(root == null) return new ArrayList<>(new ArrayList<>());
        Queue<TreeNode> q = new ArrayDeque<TreeNode>();
        List<List<Integer>> res = new ArrayList<>(); 
        q.offer(root);
        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> sub = new ArrayList<>();
            while(size-- > 0){
                TreeNode r = q.poll();
                sub.add(r.val);
                if(r.left != null) q.offer(r.left);
                if(r.right != null) q.offer(r.right);
            }
            res.add(sub);
        }
        Collections.reverse(res);
        return res;
    }

}
```