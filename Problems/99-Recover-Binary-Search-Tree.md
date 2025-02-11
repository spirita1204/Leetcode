# 99. Recover Binary Search Tree

Methods: Basic logic
Difficulty: Medium

非最優解

You are given the `root` of a binary search tree (BST), where the values of **exactly** two nodes of the tree were swapped by mistake. *Recover the tree without changing its structure*.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)

```
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg](https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg)

```
Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.

```

**Constraints:**

- The number of nodes in the tree is in the range `[2, 1000]`.
- `231 <= Node.val <= 231 - 1`

**Follow up:**

A solution using

```
O(n)
```

space is pretty straight-forward. Could you devise a constant

```
O(1)
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
    int index = 0;
    public void recoverTree(TreeNode root) {
        if(root == null) return;
        TreeNode rootCopy = root;
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        Collections.sort(res);
        insert(rootCopy, res);
    }
    public void inorder(TreeNode root, List<Integer> res){
        if(root == null) return;
        inorder(root.left, res);
        res.add(root.val);
        inorder(root.right, res);
    }
    public void insert(TreeNode root, List<Integer> res){
        if(root == null) return;
        insert(root.left, res);
        root.val = res.get(index++);
        insert(root.right, res);
    }
}
```

高級方法

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/recover-binary-search-tree/solutions/1962981/idea-inorder-traversal-easy-to-understand/?orderBy=most_votes)

```java
class Solution {//高級解法
    TreeNode prev=null,first=null,second=null;
    void inorder(TreeNode root){
        if(root==null)
            return ;
        inorder(root.left);
        if(prev!=null&&root.val<prev.val){
            if(first==null)
                first=prev;
            second=root;
        }
        prev=root;
        inorder(root.right);
    }
    public void recoverTree(TreeNode root) {
        if(root==null)
            return ; 
        inorder(root);
        int temp=first.val;
        first.val=second.val;
        second.val=temp;
    }
}
```