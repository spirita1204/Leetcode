# 1457. Pseudo-Palindromic Paths in a Binary Tree

Methods: DFS
Data structure: Set
Difficulty: Medium

Solved

Medium

Topics

Companie

Given a binary tree where node values are digits from 1 to 9. A path in the binary tree is said to be **pseudo-palindromic** if at least one permutation of the node values in the path is a palindrome.

*Return the number of **pseudo-palindromic** paths going from the root node to leaf nodes.*

**Example 1:**

![https://assets.leetcode.com/uploads/2020/05/06/palindromic_paths_1.png](https://assets.leetcode.com/uploads/2020/05/06/palindromic_paths_1.png)

```
Input: root = [2,3,1,3,1,null,1]
Output: 2
Explanation: The figure above represents the given binary tree. There are three paths going from the root node to leaf nodes: the red path [2,3,3], the green path [2,1,1], and the path [2,3,1]. Among these paths only red path and green path are pseudo-palindromic paths since the red path [2,3,3] can be rearranged in [3,2,3] (palindrome) and the green path [2,1,1] can be rearranged in [1,2,1] (palindrome).

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/05/07/palindromic_paths_2.png](https://assets.leetcode.com/uploads/2020/05/07/palindromic_paths_2.png)

```
Input: root = [2,1,1,1,3,null,null,null,null,null,1]
Output: 1
Explanation: The figure above represents the given binary tree. There are three paths going from the root node to leaf nodes: the green path [2,1,1], the path [2,1,3,1], and the path [2,1]. Among these paths only the green path is pseudo-palindromic since [2,1,1] can be rearranged in [1,2,1] (palindrome).

```

**Example 3:**

```
Input: root = [9]
Output: 1

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `1 <= Node.val <= 9`

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
    public int pseudoPalindromicPaths (TreeNode root) {
        // DFS
        return dfs(root, new HashSet());
    }

    private int dfs(TreeNode root, Set<Integer> numbers) {
        if(root == null) {
            return 0;
        }
        if(numbers.contains(root.val)) {
            numbers.remove(root.val);
        }else {
            numbers.add(root.val);
        }
        if(root.left == null && root.right == null) {// leaf
            return numbers.size() <= 1 ? 1 : 0;// 1代表符合
        }
        int left = dfs(root.left, new HashSet(numbers));// new 避免set互相干擾
        int right = dfs(root.right, new HashSet(numbers));
        
        return left + right;
    }
}
```