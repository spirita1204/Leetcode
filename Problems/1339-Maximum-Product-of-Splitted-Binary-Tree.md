# 1339. Maximum Product of Splitted Binary Tree  

  Methods: DFS,BFS </br> Difficulty: Medium </br> </br>Given the `root` of a binary tree, split the binary tree into two subtrees by removing one edge such that the product of the sums of the subtrees is maximized.  

Return *the maximum product of the sums of the two subtrees*. Since the answer may be too large, return it **modulo** `109 + 7`.

**Note** that you need to maximize the answer before taking the mod and not after taking it.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/01/21/sample_1_1699.png)

```plain text
Input: root = [1,2,3,4,5,6]
Output: 110
Explanation: Remove the red edge and get 2 binary trees with sum 11 and 10. Their product is 110 (11*10)
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2020/01/21/sample_2_1699.png)

```plain text
Input: root = [1,null,2,3,4,null,null,5,6]
Output: 90
Explanation: Remove the red edge and get 2 binary trees with sum 15 and 6.Their product is 90 (15*6)
```

**Constraints:**

- The number of nodes in the tree is in the range `[2, 5 * 104]`.
- `1 <= Node.val <= 104`
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
    long MOD = 1000000007L;
    long ans = 0;

    private long dfs(TreeNode node) {
        if (node == null)
            return 0;

        node.val += (dfs(node.left) + dfs(node.right));
        return node.val;
    }

    public int maxProduct(TreeNode root) {
        long total = dfs(root);

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node == null)
                continue;

            long cur = (total - node.val) * node.val;
            ans = Math.max(ans, cur);

            if (node.left != null)
                q.offer(node.left);
            if (node.right != null)
                q.offer(node.right);
        }

        return (int) (ans % MOD);
    }
}
```

