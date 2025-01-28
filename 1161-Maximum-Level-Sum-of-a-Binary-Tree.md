# 1161. Maximum Level Sum of a Binary Tree

Methods: BFS
Difficulty: Medium

Given the `root` of a binary tree, the level of its root is `1`, the level of its children is `2`, and so on.

Return the **smallest** level `x` such that the sum of all the values of nodes at level `x` is **maximal**.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/05/03/capture.JPG](https://assets.leetcode.com/uploads/2019/05/03/capture.JPG)

```
Input: root = [1,7,0,7,-8,null,null]
Output: 2
Explanation:
Level 1 sum = 1.
Level 2 sum = 7 + 0 = 7.
Level 3 sum = 7 + -8 = -1.
So we return the level with the maximum sum which is level 2.

```

**Example 2:**

```
Input: root = [989,null,10250,98693,-89388,null,null,null,-32127]
Output: 2

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `105 <= Node.val <= 105`

```java
//problem 1161
class Solution {
    public int maxLevelSum(TreeNode root) {
        int level = 1, res = 1, maxSum = Integer.MIN_VALUE;
        Queue<TreeNode> q = new ArrayDeque<TreeNode>();
        q.offer(root);
        while (!q.isEmpty()) {            
            int sum = 0;            
            for (int cnt = q.size(); cnt > 0; cnt--) {
                TreeNode n = q.poll();
                sum += n.val;
                if (n.left != null) q.offer(n.left);
                if (n.right != null) q.offer(n.right);
            }
            
            if (sum > maxSum) {
                maxSum = sum;
                res = level;
            }
            
            level++;
        }
        return res;
    }
}
```