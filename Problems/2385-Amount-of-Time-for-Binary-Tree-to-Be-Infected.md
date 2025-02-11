# 2385. Amount of Time for Binary Tree to Be Infected

Methods: DFS
Data structure: Graph, Hash Table
Difficulty: Medium++

Medium

Topics

Companies

Hint

You are given the `root` of a binary tree with **unique** values, and an integer `start`. At minute `0`, an **infection** starts from the node with value `start`.

Each minute, a node becomes infected if:

- The node is currently uninfected.
- The node is adjacent to an infected node.

Return *the number of minutes needed for the entire tree to be infected.*

**Example 1:**

![https://assets.leetcode.com/uploads/2022/06/25/image-20220625231744-1.png](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231744-1.png)

```
Input: root = [1,5,3,null,4,10,6,9,2], start = 3
Output: 4
Explanation: The following nodes are infected during:
- Minute 0: Node 3
- Minute 1: Nodes 1, 10 and 6
- Minute 2: Node 5
- Minute 3: Node 4
- Minute 4: Nodes 9 and 2
It takes 4 minutes for the whole tree to be infected so we return 4.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/06/25/image-20220625231812-2.png](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231812-2.png)

```
Input: root = [1], start = 1
Output: 0
Explanation: At minute 0, the only node in the tree is infected so we return 0.

```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `1 <= Node.val <= 105`
- Each node has a **unique** value.
- A node with a value of `start` exists in the tree.

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
    // Start node for BFS
    TreeNode origin;

    public int amountOfTime(TreeNode root, int start) {
        // 將樹轉graph 再從start用bfs遍歷
        Map<TreeNode, TreeNode> hm = new HashMap<>();
        Queue<TreeNode> q = new LinkedList<>();    
        Set<TreeNode> visited = new HashSet<>();
        int time = 0;

        treeToGraphDFS(root, start, hm);
        // 定義start為起點
        q.offer(origin);
        
        while(!q.isEmpty()){
            int size = q.size();
            while(size-- > 0){
                TreeNode node = q.poll();
                visited.add(node);
                // 往左子樹走
                if(node.left != null && !visited.contains(node.left)) q.offer(node.left);
                // 往右子樹走
                if(node.right != null && !visited.contains(node.right)) q.offer(node.right);
                // 往parent走
                if(hm.containsKey(node) && !visited.contains(hm.get(node))) q.offer(hm.get(node));
            }
            time++;
        }
        return time-  1;
    }

    // map (child->parent)
    private void treeToGraphDFS(TreeNode root, int start, Map<TreeNode, TreeNode> hm){
        if(root == null) return;
        
        if(root.left != null) hm.put(root.left, root);
        if(root.right != null) hm.put(root.right, root);
        
		// Defining start node for BFS
        if(root.val == start) origin = root;
        
        treeToGraphDFS(root.left, start, hm);
        treeToGraphDFS(root.right, start, hm);
    }
}
```