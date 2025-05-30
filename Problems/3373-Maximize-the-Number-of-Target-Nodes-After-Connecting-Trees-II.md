# 3373. Maximize the Number of Target Nodes After Connecting Trees II  

  Methods: DFS </br> Data Structure: Graph </br> Difficulty: Hard </br> Similar: 3372 </br> </br>There exist two **undirected **trees with `n` and `m` nodes, labeled from `[0, n - 1]` and `[0, m - 1]`, respectively. 

You are given two 2D integer arrays `edges1` and `edges2` of lengths `n - 1` and `m - 1`, respectively, where `edges1[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the first tree and `edges2[i] = [ui, vi]` indicates that there is an edge between nodes `ui` and `vi` in the second tree.

Node `u` is **target** to node `v` if the number of edges on the path from `u` to `v` is even. **Note** that a node is *always* **target** to itself.

Return an array of `n` integers `answer`, where `answer[i]` is the **maximum** possible number of nodes that are **target** to node `i` of the first tree if you had to connect one node from the first tree to another node in the second tree.

**Note** that queries are independent from each other. That is, for every query you will remove the added edge before proceeding to the next query.

**Example 1:**

**Input:** edges1 = [[0,1],[0,2],[2,3],[2,4]], edges2 = [[0,1],[0,2],[0,3],[2,7],[1,4],[4,5],[4,6]]

**Output:** [8,7,7,8,8]

**Explanation:**

- For `i = 0`, connect node 0 from the first tree to node 0 from the second tree.
- For `i = 1`, connect node 1 from the first tree to node 4 from the second tree.
- For `i = 2`, connect node 2 from the first tree to node 7 from the second tree.
- For `i = 3`, connect node 3 from the first tree to node 0 from the second tree.
- For `i = 4`, connect node 4 from the first tree to node 4 from the second tree.
![Image](https://assets.leetcode.com/uploads/2024/09/24/3982-1.png)

**Example 2:**

**Input:** edges1 = [[0,1],[0,2],[0,3],[0,4]], edges2 = [[0,1],[1,2],[2,3]]

**Output:** [3,6,6,6,6]

**Explanation:**

For every `i`, connect node `i` of the first tree with any node of the second tree.

![Image](https://assets.leetcode.com/uploads/2024/09/24/3928-2.png)

**Constraints:**

- `2 <= n, m <= 105`
- `edges1.length == n - 1`
- `edges2.length == m - 1`
- `edges1[i].length == edges2[i].length == 2`
- `edges1[i] = [ai, bi]`
- `0 <= ai, bi < n`
- `edges2[i] = [ui, vi]`
- `0 <= ui, vi < m`
- The input is generated such that `edges1` and `edges2` represent valid trees.
```java
class Solution {
    int evenA, oddA, evenB, oddB;

    public int[] maxTargetNodes(int[][] edges1, int[][] edges2) {
        List<List<Integer>> adjA = buildList(edges1);
        List<List<Integer>> adjB = buildList(edges2);

        int n = adjA.size();
        int m = adjB.size();

        int[] colorA = new int[n];
        int[] colorB = new int[m];

        Arrays.fill(colorA, -1);
        Arrays.fill(colorB, -1);
        
        colorA[0] = 0;
        dfsColor(adjA, 0, -1, colorA, true);
        colorB[0] = 0;
        dfsColor(adjB, 0, -1, colorB, false);

        int maxiB = Math.max(evenB, oddB);
        int[] res = new int[n];
        System.out.println(evenA);
        System.out.println(oddA);
        for (int i = 0; i < n; i++)
            res[i] = (colorA[i] == 0 ? evenA : oddA) + maxiB;

        return res;
    }

    private List<List<Integer>> buildList(int[][] edges) {
        int n = edges.length + 1;
        List<List<Integer>> adj = new ArrayList<>();

        for (int i = 0; i < n; i++) 
            adj.add(new ArrayList<>());
        for (int[] e : edges) {
            adj.get(e[0]).add(e[1]);
            adj.get(e[1]).add(e[0]);
        }
        return adj;
    }

    private void dfsColor(List<List<Integer>> adj, int u, int parent, int[] color, boolean isA) {
        if (color[u] == 0) {
            if (isA) evenA++;
            else evenB++;
        } else {
            if (isA) oddA++;
            else oddB++;
        }
        for (int v : adj.get(u)) 
            if (v != parent) {
                color[v] = color[u] ^ 1;
                dfsColor(adj, v, u, color, isA);
            }
    }
}
```

