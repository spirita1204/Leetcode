# 3203. Find Minimum Diameter After Merging Two Trees

Data structure: Graph

There exist two **undirected** trees with `n` and `m` nodes, numbered from `0` to `n - 1` and from `0` to `m - 1`, respectively. You are given two 2D integer arrays `edges1` and `edges2` of lengths `n - 1` and `m - 1`, respectively, where `edges1[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the first tree and `edges2[i] = [ui, vi]` indicates that there is an edge between nodes `ui` and `vi` in the second tree.

You must connect one node from the first tree with another node from the second tree with an edge.

Return the **minimum** possible **diameter** of the resulting tree.

The **diameter** of a tree is the length of the *longest* path between any two nodes in the tree.

**Example 1:**

![https://assets.leetcode.com/uploads/2024/04/22/example11-transformed.png](https://assets.leetcode.com/uploads/2024/04/22/example11-transformed.png)

**Input:** edges1 = [[0,1],[0,2],[0,3]], edges2 = [[0,1]]

**Output:** 3

**Explanation:**

We can obtain a tree of diameter 3 by connecting node 0 from the first tree with any node from the second tree.

**Example 2:**

![https://assets.leetcode.com/uploads/2024/04/22/example211.png](https://assets.leetcode.com/uploads/2024/04/22/example211.png)

**Input:** edges1 = [[0,1],[0,2],[0,3],[2,4],[2,5],[3,6],[2,7]], edges2 = [[0,1],[0,2],[0,3],[2,4],[2,5],[3,6],[2,7]]

**Output:** 5

**Explanation:**

We can obtain a tree of diameter 5 by connecting node 0 from the first tree with node 0 from the second tree.

**Constraints:**

- `1 <= n, m <= 105`
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
    public int minimumDiameterAfterMerge(int[][] edges1, int[][] edges2) {
        // 計算兩棵樹的直徑
        int diameter1 = calculateDiameter(edges1);
        int diameter2 = calculateDiameter(edges2);

        // 計算半徑（直徑的一半，向上取整）
        int radius1 = (diameter1 + 1) / 2;
        int radius2 = (diameter2 + 1) / 2;

        // 合併後的最小直徑
        return Math.max(diameter1, Math.max(diameter2, radius1 + radius2 + 1));
    }

    // 計算樹的直徑
    private int calculateDiameter(int[][] edges) {
        int n = edges.length + 1; // 節點數量
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
        }

        // 透過 BFS 找到直徑
        int[] farthestFromAny = bfs(0, adj);         // 第一次 BFS，找到最遠的節點
        int farthestNode = farthestFromAny[0];
        int[] farthestFromFarthest = bfs(farthestNode, adj); // 第二次 BFS，找直徑

        return farthestFromFarthest[1];
    }

    // BFS 用於找到最遠的節點與距離
    private int[] bfs(int start, List<List<Integer>> adj) {
        int n = adj.size();
        boolean[] visited = new boolean[n];
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{start, 0});
        visited[start] = true;

        int farthestNode = start;
        int maxDistance = 0;

        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int node = curr[0];
            int distance = curr[1];

            if (distance > maxDistance) {
                maxDistance = distance;
                farthestNode = node;
            }

            for (int neighbor : adj.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(new int[]{neighbor, distance + 1});
                }
            }
        }

        return new int[]{farthestNode, maxDistance};
    }
}

```