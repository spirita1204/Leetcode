# 3650. Minimum Cost Path with Edge Reversals  

  Methods: Shortest Path </br> Difficulty: Medium </br> </br>You are given a directed, weighted graph with `n` nodes labeled from 0 to `n - 1`, and an array `edges` where `edges[i] = [ui, vi, wi]` represents a directed edge from node `ui` to node `vi` with cost `wi`.

Each node `ui` has a switch that can be used **at most once**: when you arrive at `ui` and have not yet used its switch, you may activate it on one of its incoming edges `vi → ui` reverse that edge to `ui → vi` and **immediately** traverse it.

The reversal is only valid for that single move, and using a reversed edge costs `2 * wi`.

Return the **minimum** total cost to travel from node 0 to node `n - 1`. If it is not possible, return -1.

**Example 1:**

**Input:** n = 4, edges = [[0,1,3],[3,1,1],[2,3,4],[0,2,2]]

**Output:** 5

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/05/07/e1drawio.png)

- Use the path `0 → 1` (cost 3).
- At node 1 reverse the original edge `3 → 1` into `1 → 3` and traverse it at cost `2 * 1 = 2`.
- Total cost is `3 + 2 = 5`.
**Example 2:**

**Input:** n = 4, edges = [[0,2,1],[2,1,1],[1,3,1],[2,3,3]]

**Output:** 3

**Explanation:**

- No reversal is needed. Take the path `0 → 2` (cost 1), then `2 → 1` (cost 1), then `1 → 3` (cost 1).
- Total cost is `1 + 1 + 1 = 3`.
**Constraints:**

- `2 <= n <= 5 * 104`
- `1 <= edges.length <= 105`
- `edges[i] = [ui, vi, wi]`
- `0 <= ui, vi <= n - 1`
- `1 <= wi <= 1000`  
```java
class Solution {
    public int minCost(int n, int[][] edges) {
        // Building augmented graph
        ArrayList<int[]>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) 
            adj[i] = new ArrayList<>();

        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0], v = edges[i][1], w = edges[i][2];
            adj[u].add(new int[]{v, w});
            adj[v].add(new int[]{u, 2 * w});
        }

        // Initialize distance array from 0 node
        final int INF = 1000000000;
        int[] dist = new int[n];
        for (int i = 0; i < n; i++) 
            dist[i] = INF;
        dist[0] = 0;

        // Dijkstra(每次都從目前距離最小的點開始擴展)
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        pq.add(new int[]{0, 0});// [目前到這個點的最短距離, 節點編號] min heap

        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int d = cur[0];// 從起點 0 到 u 的距離（候選值）
            int u = cur[1];// 目前要處理的節點
            if (u == n - 1)  // Early exit
                return d;
            if (d != dist[u])  // Stale edge跳過「過期狀態」
                continue;
            // 嘗試用 u 當中繼點，更新鄰居（Relaxation）
            for (int i = 0; i < adj[u].size(); i++) {
                int[] e = adj[u].get(i);
                int v = e[0], w = e[1];
                if (dist[u] + w < dist[v]) {  // Edge relaxation
                    dist[v] = dist[u] + w;
                    pq.add(new int[]{dist[v], v});
                }
            }
        }

        return -1;
    }
}
```

