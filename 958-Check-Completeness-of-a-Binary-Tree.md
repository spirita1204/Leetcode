# 958. Check Completeness of a Binary Tree

Methods: BFS
Difficulty: Medium

Given the `root` of a binary tree, determine if it is a *complete binary tree*.

In a [**complete binary tree**](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees), every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-1.png](https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-1.png)

```
Input: root = [1,2,3,4,5,6]
Output: true
Explanation: Every level before the last is full (ie. levels with node-values {1} and {2, 3}), and all nodes in the last level ({4, 5, 6}) are as far left as possible.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-2.png](https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-2.png)

```
Input: root = [1,2,3,4,5,null,7]
Output: false
Explanation: The node with value 7 isn't as far left as possible.

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 100]`.
- `1 <= Node.val <= 1000`

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
    public boolean isCompleteTree(TreeNode root) { // attention this situation ex: [1,2,3,5,null,7,8]
        Queue<TreeNode> q = new ArrayDeque<>();
        boolean haveRight = true;
        q.offer(root);

        while(!q.isEmpty()){
            TreeNode sub = q.poll();
            if(sub.left != null){// have left 
                q.offer(sub.left);
                if(haveRight == false) return false;
                if(sub.right != null){ // have right
                    q.offer(sub.right);
                }else{
                    haveRight = false;
                }
            }else if(sub.left == null && sub.right != null){//not complete
                return false;
            }else if(sub.left == null && sub.right == null){
                haveRight = false;
            }
        }
        return true;
    }
}958. Check Completeness of a Binary Tree
```