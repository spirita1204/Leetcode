# 1110. Delete Nodes And Return Forest

Methods: DFS, Order Traversal
Data structure: Set
Difficulty: Medium

Medium

Topics

Companies

Given the `root` of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in `to_delete`, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/07/01/screen-shot-2019-07-01-at-53836-pm.png](https://assets.leetcode.com/uploads/2019/07/01/screen-shot-2019-07-01-at-53836-pm.png)

```
Input: root = [1,2,3,4,5,6,7], to_delete = [3,5]
Output: [[1,2,null,4],[6],[7]]

```

**Example 2:**

```
Input: root = [1,2,4,null,3], to_delete = [3]
Output: [[1,2,4]]

```

**Constraints:**

- The number of nodes in the given tree is at most `1000`.
- Each node has a distinct value between `1` and `1000`.
- `to_delete.length <= 1000`
- `to_delete` contains distinct values between `1` and `1000`.

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
    List<TreeNode> res = new ArrayList<>();

    public List<TreeNode> delNodes(TreeNode root, int[] to_delete) {
        Set<Integer> deletes = new HashSet<>();
        int val = root.val;
        for(int i: to_delete) 
            deletes.add(i);

        TreeNode r = dfs(root, deletes);
        // 當最後回傳回來都正常 則把原本root 也加進去res
        if(r != null && r.val == val) 
            res.add(r);

        return res;
    }
    private TreeNode dfs(TreeNode root, Set<Integer> deletes) {
        // 左 右 上
        // postorder ensures we handle children before their parent nodes
        if(root == null) return null;

        TreeNode left = dfs(root.left, deletes);
        TreeNode right =  dfs(root.right, deletes);
        // 如果需刪除 則把child先處理掉 
        if(deletes.contains(root.val)) {
            root = null;
            if(left != null) res.add(left);
            if(right != null) res.add(right);
        } else {
            root.left = left;
            root.right = right;
        }
        return root;
    }
}
```