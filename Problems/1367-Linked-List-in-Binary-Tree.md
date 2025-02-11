# 1367. Linked List in Binary Tree

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

Given a binary tree `root` and a linked list with `head` as the first node.

Return True if all the elements in the linked list starting from the `head` correspond to some *downward path* connected in the binary tree otherwise return False.

In this context downward path means a path that starts at some node and goes downwards.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/02/12/sample_1_1720.png](https://assets.leetcode.com/uploads/2020/02/12/sample_1_1720.png)

```
Input: head = [4,2,8], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
Output: true
Explanation: Nodes in blue form a subpath in the binary Tree.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/02/12/sample_2_1720.png](https://assets.leetcode.com/uploads/2020/02/12/sample_2_1720.png)

```
Input: head = [1,4,2,6], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
Output: true

```

**Example 3:**

```
Input: head = [1,4,2,6,8], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
Output: false
Explanation: There is no path in the binary tree that contains all the elements of the linked list fromhead.

```

**Constraints:**

- The number of nodes in the tree will be in the range `[1, 2500]`.
- The number of nodes in the list will be in the range `[1, 100]`.
- `1 <= Node.val <= 100` for each node in the linked list and binary tree.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
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
    public boolean isSubPath(ListNode head, TreeNode root) {
        if(root == null) return false;
        if(head.val == root.val && dfs(head, root)) return true;
        
        return isSubPath(head, root.left) || isSubPath(head, root.right);
    }
    private boolean dfs(ListNode head, TreeNode root) {
        if(root == null)    
            return head == null;// 剛好都用完
        if(head == null) 
            return true;// 提早找完
        if(root.val != head.val) 
            return false;
        boolean left = dfs(head.next, root.left);
        boolean right = dfs(head.next, root.right);

        return left || right;
    }
}
```