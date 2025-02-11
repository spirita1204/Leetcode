# 1325. Delete Leaves With a Given Value

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a binary tree `root` and an integer `target`, delete all the **leaf nodes** with value `target`.

Note that once you delete a leaf node with value `target`**,** if its parent node becomes a leaf node and has the value `target`, it should also be deleted (you need to continue doing that until you cannot).

**Example 1:**

![https://assets.leetcode.com/uploads/2020/01/09/sample_1_1684.png](https://assets.leetcode.com/uploads/2020/01/09/sample_1_1684.png)

```
Input: root = [1,2,3,2,null,2,4], target = 2
Output: [1,null,3,null,4]
Explanation: Leaf nodes in green with value (target = 2) are removed (Picture in left).
After removing, new nodes become leaf nodes with value (target = 2) (Picture in center).

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/01/09/sample_2_1684.png](https://assets.leetcode.com/uploads/2020/01/09/sample_2_1684.png)

```
Input: root = [1,3,3,3,2], target = 3
Output: [1,3,null,null,2]

```

**Example 3:**

![https://assets.leetcode.com/uploads/2020/01/15/sample_3_1684.png](https://assets.leetcode.com/uploads/2020/01/15/sample_3_1684.png)

```
Input: root = [1,2,null,2,null,2], target = 2
Output: [1]
Explanation: Leaf nodes in green with value (target = 2) are removed at each step.

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 3000]`.
- `1 <= Node.val, target <= 1000`

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
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        boolean rootV = dfs(root, target);
        if (rootV)
            return null;// 當root也是要刪除的target

        return root;
    }

    private boolean dfs(TreeNode root, int target) {
        if (root == null)
            return true;

        boolean left = dfs(root.left, target);
        boolean right = dfs(root.right, target);

        if (left)
            root.left = null;
        if (right)
            root.right = null;
        if (left && right && root.val == target) {// 當前要刪除 告訴上一層可以讓其變null
            return true;
        }
        return false;
    }
}
```