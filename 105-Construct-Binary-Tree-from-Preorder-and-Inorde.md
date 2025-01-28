# 105. Construct Binary Tree from Preorder and Inorder Traversal

Methods: DFS
Difficulty: Medium

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return *the binary tree*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/tree.jpg](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

```

**Example 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]

```

**Constraints:**

- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` and `inorder` consist of **unique** values.
- Each value of `inorder` also appears in `preorder`.
- `preorder` is **guaranteed** to be the preorder traversal of the tree.
- `inorder` is **guaranteed** to be the inorder traversal of the tree.

```jsx
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        /*
        The basic idea is to take the last element in postorder array as the root,
        find the position of the root in the inorder array; 
        then locate the range for left sub-tree and right sub-tree and do recursion. 
        Use a HashMap to record the index of root in the inorder array.
        */
	    HashMap<Integer, Integer> hm = new HashMap<Integer,Integer>();//對應inorder位置做編碼
	    for (int i = 0 ; i < inorder.length ; i++)
		    hm.put(inorder[i], i);
        return buildSubTree(inorder, 0, inorder.length-1, preorder, 0, preorder.length-1,hm);
    }
    public TreeNode buildSubTree(int[] inorder,int inorderStart, int inorderEnd, int[] preorder, int preorderStart, int preorderEnd, HashMap<Integer,Integer> hm) {
        if(preorderStart > preorderEnd || inorderStart > inorderEnd) return null;//填null
        TreeNode root = new TreeNode(preorder[preorderStart]);//定位root 
        int inorderIndex = hm.get(preorder[preorderStart]);//定位root在inorder arr中座標
        TreeNode leftTree = buildSubTree(inorder, inorderStart, inorderIndex - 1, preorder, preorderStart + 1, preorderStart + 1 + inorderIndex - inorderStart - 1, hm);
        //                                                                                                  
        TreeNode rightTree = buildSubTree(inorder, inorderIndex + 1, inorderEnd, preorder, preorderStart + 1 + inorderIndex - inorderStart, preorderEnd, hm);
        //                                                                        
        root.left = leftTree;//塞左leaf
        root.right = rightTree;//塞右leaf
        return root;
    }
}
```