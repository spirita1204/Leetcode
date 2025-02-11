# 1530. Number of Good Leaf Nodes Pairs

Methods: DFS, Order Traversal
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given the `root` of a binary tree and an integer `distance`. A pair of two different **leaf** nodes of a binary tree is said to be good if the length of **the shortest path** between them is less than or equal to `distance`.

Return *the number of good leaf node pairs* in the tree.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/07/09/e1.jpg](https://assets.leetcode.com/uploads/2020/07/09/e1.jpg)

```
Input: root = [1,2,3,null,4], distance = 3
Output: 1
Explanation: The leaf nodes of the tree are 3 and 4 and the length of the shortest path between them is 3. This is the only good pair.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/07/09/e2.jpg](https://assets.leetcode.com/uploads/2020/07/09/e2.jpg)

```
Input: root = [1,2,3,4,5,6,7], distance = 3
Output: 2
Explanation: The good pairs are [4,5] and [6,7] with shortest path = 2. The pair [4,6] is not good because the length of ther shortest path between them is 4.

```

**Example 3:**

```
Input: root = [7,1,4,6,null,5,3,null,null,null,null,null,2], distance = 3
Output: 1
Explanation: The only good pair is [2,5].

```

**Constraints:**

- The number of nodes in the `tree` is in the range `[1, 210].`
- `1 <= Node.val <= 100`
- `1 <= distance <= 10`

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
    int res = 0;
    public int countPairs(TreeNode root, int distance) {
        // 用拎袋子的最上面來看 左右兩邊相加
        // distance <= 10 可以給定陣列int[11]
        //      ^
        //    /   \
        // [2,2]  [2,2]
        dfs(root, distance);
        
        return res;
    }

    private int[] dfs(TreeNode root, int distance) {
        if(root == null) return null;
        // 紀錄長度各數
        int[] childs = new int[11];
        // postorder 先處理子節點
        int[] left = dfs(root.left, distance);
        int[] right = dfs(root.right, distance);
        // leaf 則代表長度1
        if(left == null && right == null) {
            childs[1] = 1;
				    return childs;
        }
        // 找出所有滿足條件組合
        if(left != null && right != null) { 
            for (int i = 0; i < 11; i++) {
                for (int j = 0; j < 11; j++) {
                    if (i + j <= distance) // pruning
                        res += (left[i] * right[j]);// 左達標數量*右達標數量
                }
            }
        }
        // 給下一層使用 + 1, 組合
        for(int i = 0; i < 10; i++) {// 10+1超過條件
            if(left != null)
                childs[i + 1] += left[i];
            if(right != null)
                childs[i + 1] += right[i];
        }
        return childs;
    }
}
```