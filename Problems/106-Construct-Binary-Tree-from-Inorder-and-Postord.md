# 106. Construct Binary Tree from Inorder and Postorder Traversal

Data structure: Hash Table
Methods: DFS
Difficulty: Medium

- DFS
- HashMap

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return *the binary tree*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/02/19/tree.jpg](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
Output: [3,9,20,null,null,15,7]

```

**Example 2:**

```
Input: inorder = [-1], postorder = [-1]
Output: [-1]
```

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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        /*
        The basic idea is to take the last element in postorder array as the root,
        find the position of the root in the inorder array; 
        then locate the range for left sub-tree and right sub-tree and do recursion. 
        Use a HashMap to record the index of root in the inorder array.
        */
	    HashMap<Integer, Integer> hm = new HashMap<Integer,Integer>();//對應inorder位置做編碼
	    for (int i = 0 ; i < inorder.length ; i++)
		    hm.put(inorder[i], i);
        return buildSubTree(inorder, 0, inorder.length-1, postorder, 0, postorder.length-1,hm);
    }
    public TreeNode buildSubTree(int[] inorder,int inorderStart, int inorderEnd, int[] postorder, int postorderStart, int postorderEnd, HashMap<Integer,Integer> hm) {
        if(postorderStart > postorderEnd || inorderStart > inorderEnd) return null;//填null
        TreeNode root = new TreeNode(postorder[postorderEnd]);//定位root 
        int inorderIndex = hm.get(postorder[postorderEnd]);//定位root在inorder arr中座標
        TreeNode leftTree = buildSubTree(inorder, inorderStart, inorderIndex - 1, postorder, postorderStart, postorderStart + inorderIndex - inorderStart - 1, hm);
        //                                                                                                   左邊子術postorder範圍
        TreeNode rightTree = buildSubTree(inorder, inorderIndex + 1, inorderEnd, postorder, postorderStart + inorderIndex - inorderStart, postorderEnd - 1, hm);
        //                                                                                  右邊子術postorder範圍 = 左邊子術postorder範圍+1, 到root之前一個 
        root.left = leftTree;//塞左leaf
        root.right = rightTree;//塞右leaf
        return root;
    }
}
```