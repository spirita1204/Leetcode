# 1382. Balance a Binary Search Tree

Methods: Binary Search, DFS
Difficulty: Medium

Given the `root` of a binary search tree, return *a **balanced** binary search tree with the same node values*. If there is more than one answer, return **any of them**.

A binary search tree is **balanced** if the depth of the two subtrees of every node never differs by more than `1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg](https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg)

```
Input: root = [1,null,2,null,3,null,4,null,null]
Output: [2,1,3,null,null,null,4]
Explanation: This is not the only correct answer, [3,1,4,null,2] is also correct.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/08/10/balanced2-tree.jpg](https://assets.leetcode.com/uploads/2021/08/10/balanced2-tree.jpg)

```
Input: root = [2,1,3]
Output: [2,1,3]

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `1 <= Node.val <= 105`

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
    public TreeNode balanceBST(TreeNode root) {
        List<Integer> sortLists = new ArrayList<>();
        // 做出有序列
        inOrderTraversal(root, sortLists);
        // 建構平衡樹
        return build(sortLists, 0, sortLists.size() - 1);
    }
    private void inOrderTraversal(TreeNode root, List<Integer> sortLists) {
        if(root == null) return;

        inOrderTraversal(root.left, sortLists);
        sortLists.add(root.val);
        inOrderTraversal(root.right, sortLists);
    }
    // 根據BS 將資料切兩半同時給左右子樹
    private TreeNode build(List<Integer> sortLists, int l, int r) {
        if(l > r) return null;
        int mid = (l + r) / 2;
        int midVal = sortLists.get(mid);

        TreeNode root = new TreeNode(
            midVal, 
            build(sortLists, l, mid - 1),
            build(sortLists, mid + 1, r));

        return root;
    }
}
```