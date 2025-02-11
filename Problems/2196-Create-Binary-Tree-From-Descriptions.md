# 2196. Create Binary Tree From Descriptions

Methods: DFS
Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a 2D integer array `descriptions` where `descriptions[i] = [parenti, childi, isLefti]` indicates that `parenti` is the **parent** of `childi` in a **binary** tree of **unique** values. Furthermore,

- If `isLefti == 1`, then `childi` is the left child of `parenti`.
- If `isLefti == 0`, then `childi` is the right child of `parenti`.

Construct the binary tree described by `descriptions` and return *its **root***.

The test cases will be generated such that the binary tree is **valid**.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/02/09/example1drawio.png](https://assets.leetcode.com/uploads/2022/02/09/example1drawio.png)

```
Input: descriptions = [[20,15,1],[20,17,0],[50,20,1],[50,80,0],[80,19,1]]
Output: [50,20,80,15,17,19]
Explanation: The root node is the node with value 50 since it has no parent.
The resulting binary tree is shown in the diagram.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/02/09/example2drawio.png](https://assets.leetcode.com/uploads/2022/02/09/example2drawio.png)

```
Input: descriptions = [[1,2,1],[2,3,0],[3,4,1]]
Output: [1,2,null,null,3,4]
Explanation: The root node is the node with value 1 since it has no parent.
The resulting binary tree is shown in the diagram.

```

**Constraints:**

- `1 <= descriptions.length <= 104`
- `descriptions[i].length == 3`
- `1 <= parenti, childi <= 105`
- `0 <= isLefti <= 1`
- The binary tree described by `descriptions` is valid.

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
    public TreeNode createBinaryTree(int[][] descriptions) {
        Set<Integer> childrenSet = new HashSet<>();// 判斷root用
        Map<Integer, int[]> childrenHashmap = new HashMap<>();// parent-> left+right
        // 建立樹hashmap
        for (int[] desc : descriptions) {
            int parent = desc[0];
            int child = desc[1];
            boolean isLeft = (desc[2] == 1);

            childrenHashmap.putIfAbsent(parent, new int[]{-1, -1});
            childrenSet.add(child);
            if (isLeft) 
                childrenHashmap.get(parent)[0] = child;
            else 
                childrenHashmap.get(parent)[1] = child;
        }
        // 判斷root
        int rootVal = 0;
        for (int parent : childrenHashmap.keySet()) {
            if (!childrenSet.contains(parent)) {
                rootVal = parent;
                break;
            }
        }
        // 建構樹
        return constructTree(rootVal, childrenHashmap);
    }

    private TreeNode constructTree(int rootVal, Map<Integer, int[]> childrenHashmap) {
        TreeNode root = new TreeNode(rootVal);
        int[] childs = childrenHashmap.get(rootVal);
        if(childs != null && childs[0] != -1)
            root.left = constructTree(childs[0], childrenHashmap);
        if(childs != null && childs[1] != -1)
            root.right = constructTree(childs[1], childrenHashmap);

        return root;
    }
}
```