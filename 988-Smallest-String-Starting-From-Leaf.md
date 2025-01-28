# 988. Smallest String Starting From Leaf

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

You are given the `root` of a binary tree where each node has a value in the range `[0, 25]` representing the letters `'a'` to `'z'`.

Return *the **lexicographically smallest** string that starts at a leaf of this tree and ends at the root*.

As a reminder, any shorter prefix of a string is **lexicographically smaller**.

- For example, `"ab"` is lexicographically smaller than `"aba"`.

A leaf of a node is a node that has no children.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/01/30/tree1.png](https://assets.leetcode.com/uploads/2019/01/30/tree1.png)

```
Input: root = [0,1,2,3,4,3,4]
Output: "dba"

```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/01/30/tree2.png](https://assets.leetcode.com/uploads/2019/01/30/tree2.png)

```
Input: root = [25,1,3,1,3,0,2]
Output: "adz"

```

**Example 3:**

![https://assets.leetcode.com/uploads/2019/02/01/tree3.png](https://assets.leetcode.com/uploads/2019/02/01/tree3.png)

```
Input: root = [2,2,1,null,1,0,null,0]
Output: "abc"

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 8500]`.
- `0 <= Node.val <= 25`

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
    String smallestStr = "";

    public String smallestFromLeaf(TreeNode root) {
        if(root == null) return "";
        // [21]情況
        else if(root.left == null && root.right == null) return (char)('a' + root.val) + "";
        // 將每次結果反過來串起來 再用compareTo排序
        dfs(root, "", false);
        return smallestStr;
    }

    private void dfs(TreeNode root, String s, boolean isBothLeaf) {
        if (root == null) {// 
            // 避免[0,null,1]情況
            if(!isBothLeaf) return;
            if ("".equals(smallestStr))
                smallestStr = s;
            else 
                smallestStr = (smallestStr.compareTo(s) > 0) ? s : smallestStr;
            return;
        }
        // ascii a = 97
        char c = (char)('a' + root.val);

        dfs(root.left, c + s, root.left == null && root.right == null);
        dfs(root.right, c + s, root.left == null && root.right == null);

        return;
    }
}
```