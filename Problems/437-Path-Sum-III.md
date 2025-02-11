# 437. Path Sum III

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Given the `root` of a binary tree and an integer `targetSum`, return *the number of paths where the sum of the values along the path equals* `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg](https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg)

```
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.

```

**Example 2:**

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: 3

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 1000]`.
- `109 <= Node.val <= 109`
- `1000 <= targetSum <= 1000`

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
    public int pathSum(TreeNode root, int targetSum) {
        if(root == null) return 0;
        int rootSum = dfs(root, targetSum);// 包含根結點
        int leftSum = pathSum(root.left, targetSum);// 左節點數目
        int rightSum = pathSum(root.right, targetSum);// 右節點數目

        return rootSum + leftSum + rightSum;
    }
    // 避免 [1000000000,1000000000,null,294967296,null,1000000000,null,1000000000,null,1000000000]此test case overflow
    // 使用long
    private int dfs(TreeNode root, long sum) {
        if (root == null)
            return 0;
        int leftLeaf = dfs(root.left, sum - root.val);
        int rightLeaf = dfs(root.right, sum - root.val);
        
        return ((root.val == sum) ? 1 : 0) + leftLeaf + rightLeaf;
    }
}
```