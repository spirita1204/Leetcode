# 112. Path Sum

Methods: DFS
Difficulty: Easy

**Easy**

8.1K

931

Companies

Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
Output: true
Explanation: The root-to-leaf path with the target sum is shown.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
Input: root = [1,2,3], targetSum = 5
Output: false
Explanation: There two root-to-leaf paths in the tree:
(1 --> 2): The sum is 3.
(1 --> 3): The sum is 4.
There is no root-to-leaf path with sum = 5.

```

**Example 3:**

```
Input: root = [], targetSum = 0
Output: false
Explanation: Since the tree is empty, there are no root-to-leaf paths.

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `1000 <= Node.val <= 1000`
- `1000 <= targetSum <= 1000`

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
    boolean isSameSum = false;

    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null) return false;
        dfs(root, targetSum, 0);
        return isSameSum;
    }
    public void dfs(TreeNode root, int targetSum, int total){
        if(root == null) {
            if(total == targetSum) isSameSum = true;
            return;
        }
        if(root.left == null && root.right != null) dfs(root.right, targetSum, total + root.val);
        else if(root.left != null && root.right == null) dfs(root.left, targetSum, total + root.val);
        else{
            dfs(root.left, targetSum, total + root.val);
            dfs(root.right, targetSum, total + root.val);
        }
    }
}
```