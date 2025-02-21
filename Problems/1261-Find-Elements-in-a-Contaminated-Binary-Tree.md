# 1261. Find Elements in a Contaminated Binary Tree  

  Methods: DFS </br> Data Structure: Set </br> Difficulty: Medium </br> </br>Given a binary tree with the following rules:

1. `root.val == 0`
1. If `treeNode.val == x` and `treeNode.left != null`, then `treeNode.left.val == 2 * x + 1`
1. If `treeNode.val == x` and `treeNode.right != null`, then `treeNode.right.val == 2 * x + 2`
Now the binary tree is contaminated, which means all `treeNode.val` have been changed to `-1`.

Implement the `FindElements` class:

- `FindElements(TreeNode* root)` Initializes the object with a contaminated binary tree and recovers it.
- `bool find(int target)` Returns `true` if the `target` value exists in the recovered binary tree.
**Example 1:**

![Image](https://assets.leetcode.com/uploads/2019/11/06/untitled-diagram-4-1.jpg)

```plain text
Input
["FindElements","find","find"]
[[[-1,null,-1]],[1],[2]]
Output
[null,false,true]
Explanation
FindElements findElements = new FindElements([-1,null,-1]);
findElements.find(1); // return False
findElements.find(2); // return True
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2019/11/06/untitled-diagram-4.jpg)

```plain text
Input
["FindElements","find","find","find"]
[[[-1,-1,-1,-1,-1]],[1],[3],[5]]
Output
[null,true,true,false]
Explanation
FindElements findElements = new FindElements([-1,-1,-1,-1,-1]);
findElements.find(1); // return True
findElements.find(3); // return True
findElements.find(5); // return False
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2019/11/07/untitled-diagram-4-1-1.jpg)

```plain text
Input
["FindElements","find","find","find","find"]
[[[-1,null,-1,-1,null,-1]],[2],[3],[4],[5]]
Output
[null,true,false,false,true]
Explanation
FindElements findElements = new FindElements([-1,null,-1,-1,null,-1]);
findElements.find(2); // return True
findElements.find(3); // return False
findElements.find(4); // return False
findElements.find(5); // return True

```

**Constraints:**

- `TreeNode.val == -1`
- The height of the binary tree is less than or equal to `20`
- The total number of nodes is between `[1, 104]`
- Total calls of `find()` is between `[1, 104]`
- `0 <= target <= 106`
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
class FindElements {
    Set<Integer> exisits = new HashSet<>();

    public FindElements(TreeNode root) {
        // recover root.val
        root.val = 0;
        // dfs transversal
        dfs(root, root.val, 0);
    }
    
    public boolean find(int target) {
        return exisits.contains(target);
    }

    private void dfs (TreeNode root, int val, int dir) {
        if(root == null) return;
        if(dir == 1) // right leaf
            root.val = 2* val + 2;
        if(dir == -1) // left leaf
            root.val = 2* val + 1;

        exisits.add(root.val);

        dfs(root.left, root.val, -1);
        dfs(root.right, root.val, 1);
    }
}

/**
 * Your FindElements object will be instantiated and called as such:
 * FindElements obj = new FindElements(root);
 * boolean param_1 = obj.find(target);
 */
```

