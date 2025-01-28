# 662. Maximum Width of Binary Tree

Data structure: Hash Table
Difficulty: Medium

**Medium**

6.7K

922

Companies

Given the `root` of a binary tree, return *the **maximum width** of the given tree*.

The **maximum width** of a tree is the maximum **width** among all levels.

The **width** of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes that would be present in a complete binary tree extending down to that level are also counted into the length calculation.

It is **guaranteed** that the answer will in the range of a **32-bit** signed integer.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg](https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg)

```
Input: root = [1,3,2,5,3,null,9]
Output: 4
Explanation: The maximum width exists in the third level with length 4 (5,3,null,9).

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/03/14/maximum-width-of-binary-tree-v3.jpg](https://assets.leetcode.com/uploads/2022/03/14/maximum-width-of-binary-tree-v3.jpg)

```
Input: root = [1,3,2,5,null,null,9,6,null,7]
Output: 7
Explanation: The maximum width exists in the fourth level with length 7 (6,null,null,null,null,null,7).

```

**Example 3:**

![https://assets.leetcode.com/uploads/2021/05/03/width3-tree.jpg](https://assets.leetcode.com/uploads/2021/05/03/width3-tree.jpg)

```
Input: root = [1,3,2,5]
Output: 2
Explanation: The maximum width exists in the second level with length 2 (3,2).

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 3000]`.
- `100 <= Node.val <= 100`

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
    public int widthOfBinaryTree(TreeNode root) {// BFS
        if(root == null) return 0;

        int maxLen = 0;
        Queue<TreeNode> q = new LinkedList<>();
        Map<TreeNode, Integer> hm= new HashMap<>();// 存放每一節點對應代號(root = 1,...) 
        q.offer(root);
        hm.put(root, 1);// 設root 為1

        while(!q.isEmpty()){
            int size = q.size();
            int start = 0;
            int end = 0;

            // 同一層
            for(int i = size- 1; i>= 0; i--){
                TreeNode node = q.poll();
                System.out.print(node.val);
                // 對第一個 做紀錄
                if(i == size - 1) start = hm.get(node);
                // 對最後個 做紀錄 
                if(i == 0) end = hm.get(node);
                
                if(node.left != null) {
                    q.offer(node.left);
                    hm.put(node.left, hm.get(node)* 2);
                }
                if(node.right != null) {
                    q.offer(node.right);
                    hm.put(node.right, hm.get(node)* 2 + 1);
                }
            }
            maxLen = Math.max(maxLen, end - start + 1);
        }
        return maxLen;
    }
}
```