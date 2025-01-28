# 1305. All Elements in Two Binary Search Trees

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

Given two binary search trees `root1` and `root2`, return *a list containing all the integers from both trees sorted in **ascending** order*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/12/18/q2-e1.png](https://assets.leetcode.com/uploads/2019/12/18/q2-e1.png)

```
Input: root1 = [2,1,4], root2 = [1,0,3]
Output: [0,1,1,2,3,4]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/12/18/q2-e5-.png](https://assets.leetcode.com/uploads/2019/12/18/q2-e5-.png)

```
Input: root1 = [1,null,8], root2 = [8,1]
Output: [1,1,8,8]

```

**Constraints:**

- The number of nodes in each tree is in the range `[0, 5000]`.
- `105 <= Node.val <= 105`

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
    public List<Integer> getAllElements(TreeNode root1, TreeNode root2) {
        List<Integer> res = new ArrayList<>();
        inorder(root1, res);
        inorder(root2, res);
        Collections.sort(res);

        return res;
    }
    private void inorder(TreeNode root, List<Integer> res) {
        if(root == null) return;
        inorder(root.left, res);
        res.add(root.val);
        inorder(root.right, res);
    }
}
```