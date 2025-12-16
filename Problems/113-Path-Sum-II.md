# 113. Path Sum II  

  Methods: DFS </br> Difficulty: Medium </br> </br>Given the `root` of a binary tree and an integer `targetSum`, return *all ****root-to-leaf**** paths where the sum of the node values in the path equals *`targetSum`*. Each path should be returned as a list of the node ****values****, not node references*.

A **root-to-leaf** path is a path starting from the root and ending at any leaf node. A **leaf** is a node with no children.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```plain text
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22

```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```plain text
Input: root = [1,2,3], targetSum = 5
Output: []

```

**Example 3:**

```plain text
Input: root = [1,2], targetSum = 0
Output: []

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `1000 <= Node.val <= 1000`
- `1000 <= targetSum <= 1000`
```javascript
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
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(root, res, new ArrayList<Integer>(), 0, targetSum);
        return res;
    }
    public void dfs(TreeNode root, List<List<Integer>> res, List<Integer> sub, int total, int targetSum){
        if(root == null) return;
        sub.add(root.val);

        dfs(root.left, res, sub,total + root.val, targetSum);
        dfs(root.right, res, sub,total + root.val, targetSum);

        if(total  + root.val == targetSum && root.left == null && root.right == null) res.add(new ArrayList<>(sub));

        sub.remove(sub.size() - 1);
    }
}
```

