# 199. Binary Tree Right Side View

Methods: BFS
Difficulty: Medium

Medium

Topics

Companies

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return *the values of the nodes you can see ordered from top to bottom*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/14/tree.jpg](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]

```

**Example 2:**

```
Input: root = [1,null,3]
Output: [1,3]

```

**Example 3:**

```
Input: root = []
Output: []

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `100 <= Node.val <= 100`

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
    public List<Integer> rightSideView(TreeNode root) {
        if(root == null) return new ArrayList<>();

        Queue<TreeNode> q = new LinkedList<>();
        List<Integer> res = new ArrayList<>();

        q.offer(root);

        while(!q.isEmpty()){
            int size = q.size();
            while(size-- > 0){
                TreeNode sub = q.poll();
                if(sub.left != null) q.offer(sub.left);
                if(sub.right != null) q.offer(sub.right);
                if(size == 0) res.add(sub.val);
            }
        }
        return res;
    }
}
```