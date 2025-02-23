# 1028. Recover a Tree From Preorder Traversal  

  Methods: DFS </br> Difficulty: Hard </br> </br>We run a preorder depth-first search (DFS) on the `root` of a binary tree.

At each node in this traversal, we output `D` dashes (where `D` is the depth of this node), then we output the value of this node.  If the depth of a node is `D`, the depth of its immediate child is `D + 1`.  The depth of the `root` node is `0`.

If a node has only one child, that child is guaranteed to be **the left child**.

Given the output `traversal` of this traversal, recover the tree and return *its* `root`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2024/09/10/recover_tree_ex1.png)

```plain text
Input: traversal = "1-2--3--4-5--6--7"
Output: [1,2,5,3,4,6,7]
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2024/09/10/recover_tree_ex2.png)

```plain text
Input: traversal = "1-2--3---4-5--6---7"
Output: [1,2,5,3,null,6,null,4,null,7]
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2024/09/10/recover_tree_ex3.png)

```plain text
Input: traversal = "1-401--349---90--88"
Output: [1,401,null,349,88,90]
```

**Constraints:**

- The number of nodes in the original tree is in the range `[1, 1000]`.
- `1 <= Node.val <= 109`
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
    private String s;
    private int idx, level;
    
    public TreeNode recoverFromPreorder(String traversal) {
        this.s = traversal;
        this.idx = 0;
        this.level = 0;
        TreeNode node = new TreeNode(-1);
        this.helper(node, 0);
        return node.left;
    }

    private void helper(TreeNode parent, int lvl) {
        while (this.idx < this.s.length() && lvl == level) {
            int num = 0;
            while (this.idx < this.s.length() && Character.isDigit(this.s.charAt(this.idx))) {
                num = num * 10 + (this.s.charAt(this.idx++) - '0');
            }
            TreeNode node = new TreeNode(num);
            if (parent.left == null)
                parent.left = node;
            else
                parent.right = node;
            
            this.level = 0;
            while (this.idx < this.s.length() && this.s.charAt(this.idx) == '-') {
                this.level++;
                this.idx++;
            }
            this.helper(node, lvl + 1);
        }
    }
}
```

