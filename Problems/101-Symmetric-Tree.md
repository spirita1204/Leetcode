# 101. Symmetric Tree  

  Methods: BFS </br> Difficulty: Easy </br> </br>Given the `root` of a binary tree, *check whether it is a mirror of itself* (i.e., symmetric around its center).

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

```plain text
Input: root = [1,2,2,3,4,4,3]
Output: true

```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

```plain text
Input: root = [1,2,2,null,3,null,3]
Output: false

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `100 <= Node.val <= 100`
```javascript
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
	   public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> a = new ArrayDeque<>();
        Queue<TreeNode> b = new ArrayDeque<>();

        if(root.left == null && root.right == null) return true;
        else if(root.left != null && root.right == null) return false;
        else if(root.right != null & root.left == null) return false;
        a.offer(root.left);
        b.offer(root.right);
        while(!a.isEmpty() && !b.isEmpty()){
            TreeNode subA = a.poll();
            TreeNode subB = b.poll();
            if(subA.val != subB.val) return false;
            if(subA.left != null && subB.right != null){
                a.offer(subA.left);
                b.offer(subB.right);
            }else if(subA.left == null && subB.right == null){}
            else return false;

            if(subA.right != null && subB.left != null){
                a.offer(subA.right);
                b.offer(subB.left);
            }else if(subA.right == null && subB.left == null){}
            else return false;
        } 
        return true;
    }
    public boolean isSymmetric(TreeNode root) {
        TreeNode root_clone = root;
        Stack<TreeNode> a = new Stack<>();
        Stack<TreeNode> b = new Stack<>();
        a.push(root.left);
        b.push(root.right);
        if(root.left==null&&root.right==null)return true;
        root = root.left;
        root_clone = root_clone.right;
        while(true){
            if(root!=null && root_clone!=null){
                if(root.val == root_clone.val){
                    a.push(root);
                    b.push(root_clone);
                    root = root.left;
                    root_clone = root_clone.right;
                }else return false; 
            }
            else if(root==null && root_clone==null){
                if(a.isEmpty() && b.isEmpty())return true;
                root = a.pop();
                root_clone = b.pop();
                root = root.right;
                root_clone = root_clone.left;
            }
            else return false;
        } 
    }
```

