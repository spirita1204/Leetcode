# 2368. Reachable Nodes With Restrictions

Methods: DFS
Data structure: Graph
Difficulty: Medium

Medium

Topics

Companies

Hint

There is an undirected tree with `n` nodes labeled from `0` to `n - 1` and `n - 1` edges.

You are given a 2D integer array `edges` of length `n - 1` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the tree. You are also given an integer array `restricted` which represents **restricted** nodes.

Return *the **maximum** number of nodes you can reach from node* `0` *without visiting a restricted node.*

Note that node `0` will **not** be a restricted node.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/06/15/ex1drawio.png](https://assets.leetcode.com/uploads/2022/06/15/ex1drawio.png)

```
Input: n = 7, edges = [[0,1],[1,2],[3,1],[4,0],[0,5],[5,6]], restricted = [4,5]
Output: 4
Explanation: The diagram above shows the tree.
We have that [0,1,2,3] are the only nodes that can be reached from node 0 without visiting a restricted node.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/06/15/ex2drawio.png](https://assets.leetcode.com/uploads/2022/06/15/ex2drawio.png)

```
Input: n = 7, edges = [[0,1],[0,2],[0,5],[0,4],[3,2],[6,5]], restricted = [4,2,1]
Output: 3
Explanation: The diagram above shows the tree.
We have that [0,5,6] are the only nodes that can be reached from node 0 without visiting a restricted node.

```

**Constraints:**

- `2 <= n <= 105`
- `edges.length == n - 1`
- `edges[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- `edges` represents a valid tree.
- `1 <= restricted.length < n`
- `1 <= restricted[i] < n`
- All the values of `restricted` are **unique**.

```java
class Solution {
    int res = 1;
    public int reachableNodes(int n, int[][] edges, int[] restricted) {
        List<List<Integer>> adj = new ArrayList<>();
        boolean[] visited = new boolean[n];
        for(int i = 0; i < n; i++) 
            adj.add(new ArrayList<>());
        Set<Integer> hs = new HashSet<>();
        // 建構相鄰矩陣
        for(int i = 0; i < edges.length; i++) {
            adj.get(edges[i][0]).add(edges[i][1]);
            adj.get(edges[i][1]).add(edges[i][0]);
        }
        // 比對限制用
        for(int i: restricted) 
            hs.add(i);
        // 當樹狀遍歷
        visited[0] = true;
        List<Integer> root = adj.get(0);
        dfs(adj, root, hs, visited);

        return res;
    }
    private void dfs(List<List<Integer>> adj, List<Integer> root, Set<Integer> hs, boolean[] visited) {
        for(int child: root) {
            if(visited[child]) // 避免重複經過
                continue;
            if(!hs.contains(child)) {// 沒有走到限制點
                res++;
                visited[child] = true;
                dfs(adj, adj.get(child), hs, visited);
            }
        }
    }
}
```