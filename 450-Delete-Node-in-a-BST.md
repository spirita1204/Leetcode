# 450. Delete Node in a BST

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return *the **root node reference** (possibly updated) of the BST*.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

```
Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.

```

![https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg](https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg)

**Example 2:**

```
Input: root = [5,3,6,2,4,null,7], key = 0
Output: [5,3,6,2,4,null,7]
Explanation: The tree does not contain a node with value = 0.

```

**Example 3:**

```
Input: root = [], key = 0
Output: []

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `105 <= Node.val <= 105`
- Each node has a **unique** value.
- `root` is a valid binary search tree.
- `105 <= key <= 105`

**Follow up:** Could you solve it with time complexity `O(height of tree)`?

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root == null) return null;

        // 三種情境
        if(key > root.val) {
            root.right = deleteNode(root.right, key);
        } else if(key < root.val) {
            root.left = deleteNode(root.left, key);
        } else {
            // 三種情況
            if(root.left == null) {// 直接移植
                return root.right;
            } else if(root.right == null) {
                return root.left;
            } else {// 左右都存在情況，取出右側最小，再刪除
                TreeNode rightRoot = root.right;
                while(rightRoot.left != null) {
                    rightRoot = rightRoot.left;
                }
                // 將最小值給予刪除節點之點
                root.val = rightRoot.val;
                // 刪除右節點中min元素
                root.right = deleteNode(root.right, rightRoot.val);
            }
        }
        return root;
    }
}
```