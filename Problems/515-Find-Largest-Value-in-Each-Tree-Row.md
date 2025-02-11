# 515. Find Largest Value in Each Tree Row

Methods: BFS
Difficulty: Medium

Given the `root` of a binary tree, return *an array of the largest value in each row* of the tree **(0-indexed)**.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/08/21/largest_e1.jpg](https://assets.leetcode.com/uploads/2020/08/21/largest_e1.jpg)

```
Input: root = [1,3,2,5,3,null,9]
Output: [1,3,9]

```

**Example 2:**

```
Input: root = [1,2,3]
Output: [1,3]

```

**Constraints:**

- The number of nodes in the tree will be in the range `[0, 104]`.
- `231 <= Node.val <= 231 - 1`

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
    public List<Integer> largestValues(TreeNode root) {
        if(root == null)
            return new ArrayList<>();
        Queue<TreeNode> pq = new LinkedList<>();
        pq.offer(root);
        List<Integer> res = new ArrayList<>();

        while(!pq.isEmpty()) {
            int size = pq.size();
            int max = Integer.MIN_VALUE;
            while(size-- > 0) {
                TreeNode e = pq.poll();
                if(e.val > max)
                    max = e.val;
                if(e.left != null)
                    pq.offer(e.left);
                if(e.right != null)
                    pq.offer(e.right);
            }
            res.add(max);
        }
        return res;
    }
}
```