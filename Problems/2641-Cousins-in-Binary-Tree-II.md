# 2641. Cousins in Binary Tree II

Methods: BFS
Difficulty: Medium

Medium

Topics

Companies

Hint

Given the `root` of a binary tree, replace the value of each node in the tree with the **sum of all its cousins' values**.

Two nodes of a binary tree are **cousins** if they have the same depth with different parents.

Return *the* `root` *of the modified tree*.

**Note** that the depth of a node is the number of edges in the path from the root node to it.

**Example 1:**

![https://assets.leetcode.com/uploads/2023/01/11/example11.png](https://assets.leetcode.com/uploads/2023/01/11/example11.png)

```
Input: root = [5,4,9,1,10,null,7]
Output: [0,0,0,7,7,null,11]
Explanation: The diagram above shows the initial binary tree and the binary tree after changing the value of each node.
- Node with value 5 does not have any cousins so its sum is 0.
- Node with value 4 does not have any cousins so its sum is 0.
- Node with value 9 does not have any cousins so its sum is 0.
- Node with value 1 has a cousin with value 7 so its sum is 7.
- Node with value 10 has a cousin with value 7 so its sum is 7.
- Node with value 7 has cousins with values 1 and 10 so its sum is 11.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2023/01/11/diagram33.png](https://assets.leetcode.com/uploads/2023/01/11/diagram33.png)

```
Input: root = [3,1,2]
Output: [0,0,0]
Explanation: The diagram above shows the initial binary tree and the binary tree after changing the value of each node.
- Node with value 3 does not have any cousins so its sum is 0.
- Node with value 1 does not have any cousins so its sum is 0.
- Node with value 2 does not have any cousins so its sum is 0.

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `1 <= Node.val <= 104`

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
    public TreeNode replaceValueInTree(TreeNode root) {
        root.val = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()) {
            int size = q.size();
            int sum = 0;
            List<TreeNode> parent = new ArrayList<>();
            while(size-- > 0) {
                TreeNode n = q.poll();
                parent.add(n);// 供減法時用
                if(n.left != null) {
                    q.offer(n.left);
                    sum += n.left.val;
                }
                if(n.right != null) {
                    q.offer(n.right);
                    sum += n.right.val;
                }
            }
            for(TreeNode node : parent) {
                int tmp = sum;
                if(node.left != null)  tmp -= node.left.val;
                if(node.right != null) tmp -= node.right.val;
                if(node.left != null)  node.left.val = tmp;
                if(node.right != null) node.right.val = tmp;
            }
        }
        return root;
    }
}
```