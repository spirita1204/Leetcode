# 889. Construct Binary Tree from Preorder and Postorder Traversal  

  Methods: Recursion </br> Difficulty: Medium++ </br> </br>Given two integer arrays, `preorder` and `postorder` where `preorder` is the preorder traversal of a binary tree of **distinct** values and `postorder` is the postorder traversal of the same tree, reconstruct and return *the binary tree*.

If there exist multiple answers, you can **return any** of them.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg)

```plain text
Input: preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
Output: [1,2,3,4,5,6,7]
```

**Example 2:**

```plain text
Input: preorder = [1], postorder = [1]
Output: [1]
```

**Constraints:**

- `1 <= preorder.length <= 30`
- `1 <= preorder[i] <= preorder.length`
- All the values of `preorder` are **unique**.
- `postorder.length == preorder.length`
- `1 <= postorder[i] <= postorder.length`
- All the values of `postorder` are **unique**.
- It is guaranteed that `preorder` and `postorder` are the preorder traversal and postorder traversal of the same binary tree.
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
    int preIndex = 0;
    int posIndex = 0;

    public TreeNode constructFromPrePost(int[] preorder, int[] postorder) {
        TreeNode root = new TreeNode(preorder[preIndex++]);
        
        if (root.val != postorder[posIndex])
            root.left = constructFromPrePost(preorder, postorder);
        if (root.val != postorder[posIndex])
            root.right = constructFromPrePost(preorder, postorder);

        posIndex++;

        return root;
    }
}
```

