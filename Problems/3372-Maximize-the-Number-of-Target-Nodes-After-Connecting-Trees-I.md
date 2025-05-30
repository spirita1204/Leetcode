# 3372. Maximize the Number of Target Nodes After Connecting Trees I  

  Methods: BFS </br> Data Structure: Graph </br> Difficulty: Medium </br> Similar: 3373 </br> </br>There exist two **undirected **trees with `n` and `m` nodes, with **distinct** labels in ranges `[0, n - 1]` and `[0, m - 1]`, respectively.

You are given two 2D integer arrays `edges1` and `edges2` of lengths `n - 1` and `m - 1`, respectively, where `edges1[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the first tree and `edges2[i] = [ui, vi]` indicates that there is an edge between nodes `ui` and `vi` in the second tree. You are also given an integer `k`.

Node `u` is **target** to node `v` if the number of edges on the path from `u` to `v` is less than or equal to `k`. **Note** that a node is *always* **target** to itself.

Return an array of `n` integers `answer`, where `answer[i]` is the **maximum** possible number of nodes **target** to node `i` of the first tree if you have to connect one node from the first tree to another node in the second tree.

**Note** that queries are independent from each other. That is, for every query you will remove the added edge before proceeding to the next query.

**Example 1:**

**Input:** edges1 = [[0,1],[0,2],[2,3],[2,4]], edges2 = [[0,1],[0,2],[0,3],[2,7],[1,4],[4,5],[4,6]], k = 2

**Output:** [9,7,9,8,8]

**Explanation:**

- For `i = 0`, connect node 0 from the first tree to node 0 from the second tree.
- For `i = 1`, connect node 1 from the first tree to node 0 from the second tree.
- For `i = 2`, connect node 2 from the first tree to node 4 from the second tree.
- For `i = 3`, connect node 3 from the first tree to node 4 from the second tree.
- For `i = 4`, connect node 4 from the first tree to node 4 from the second tree.
![Image](https://assets.leetcode.com/uploads/2024/09/24/3982-1.png)

**Example 2:**

**Input:** edges1 = [[0,1],[0,2],[0,3],[0,4]], edges2 = [[0,1],[1,2],[2,3]], k = 1

**Output:** [6,3,3,3,3]

**Explanation:**

For every `i`, connect node `i` of the first tree with any node of the second tree.

![Image](https://assets.leetcode.com/uploads/2024/09/24/3928-2.png)

**Constraints:**

- `2 <= n, m <= 1000`
- `edges1.length == n - 1`
- `edges2.length == m - 1`
- `edges1[i].length == edges2[i].length == 2`
- `edges1[i] = [ai, bi]`
- `0 <= ai, bi < n`
- `edges2[i] = [ui, vi]`
- `0 <= ui, vi < m`
- The input is generated such that `edges1` and `edges2` represent valid trees.
- `0 <= k <= 1000`
```java
class Solution {
    public int[] maxTargetNodes(int[][] edges1, int[][] edges2, int k) {
        int n = edges1.length;
        int m = edges2.length;

        List<List<Integer>> r1 = new ArrayList<>();
        List<List<Integer>> r2 = new ArrayList<>();
        
        for (int i = 0; i <= n; i++) 
            r1.add(new ArrayList<>());
        for (int i = 0; i <= m; i++) 
            r2.add(new ArrayList<>());
        // 建表1 雙向
        for (int[] e : edges1) {
            r1.get(e[0]).add(e[1]);
            r1.get(e[1]).add(e[0]);
        }
        // 建表2 雙向
        for (int[] e : edges2) {
            r2.get(e[0]).add(e[1]);
            r2.get(e[1]).add(e[0]);
        }
        // 對圖1每一點求距離
        int[] dis1 = new int[n + 1];
        for (int i = 0; i <= n; i++) 
            dis1[i] = bfs(r1, k, i, n + 1);

        // 對圖2每一點求距離
        int dis2 = 0;
        for (int i = 0; i <= m; i++) 
            dis2 = Math.max(dis2, bfs(r2, k - 1, i, m + 1));
        
        int[] res = new int[n + 1];
        for (int i = 0; i <= n; i++) 
            res[i] = dis1[i] + dis2;

        return res;
    }
    // graph, 距離, 起點, 節點數
    private int bfs(List<List<Integer>> graph, int k, int start, int n) {
        boolean[] vis = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        int dist = 0;
        int cnt = 0;
        vis[start] = true;

        while (!q.isEmpty() && dist <= k) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int node = q.poll();
                cnt++;
                for (int neighbor : graph.get(node)) {
                    if (!vis[neighbor]) {
                        vis[neighbor] = true;
                        q.offer(neighbor);
                    }
                }
            }
            dist++;
        }
        return cnt;
    }
}
```

