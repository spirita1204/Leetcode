# Notice that the given graph may be disconnected.

  

  Methods: BFS </br> Difficulty: Hard </br> </br>

Hard

Topics

Companies

Hint

You are given a positive integer `n` representing the number of nodes in an **undirected** graph. The nodes are labeled from `1` to `n`.

You are also given a 2D integer array `edges`, where `edges[i] = [ai, bi]` indicates that there is a **bidirectional** edge between nodes `ai` and `bi`. **Notice** that the given graph may be disconnected.

Divide the nodes of the graph into `m` groups (**1-indexed**) such that:

- Each node in the graph belongs to exactly one group.
- For every pair of nodes in the graph that are connected by an edge `[ai, bi]`, if `ai` belongs to the group with index `x`, and `bi` belongs to the group with index `y`, then `|y - x| = 1`.
Return *the maximum number of groups (i.e., maximum *`m`*) into which you can divide the nodes*. Return `-1` *if it is impossible to group the nodes with the given conditions*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2022/10/13/example1.png)

```plain text
Input: n = 6, edges = [[1,2],[1,4],[1,5],[2,6],[2,3],[4,6]]
Output: 4
Explanation: As shown in the image we:
- Add node 5 to the first group.
- Add node 1 to the second group.
- Add nodes 2 and 4 to the third group.
- Add nodes 3 and 6 to the fourth group.
We can see that every edge is satisfied.
It can be shown that that if we create a fifth group and move any node from the third or fourth group to it, at least on of the edges will not be satisfied.

```

**Example 2:**

```plain text
Input: n = 3, edges = [[1,2],[2,3],[3,1]]
Output: -1
Explanation: If we add node 1 to the first group, node 2 to the second group, and node 3 to the third group to satisfy the first two edges, we can see that the third edge will not be satisfied.
It can be shown that no grouping is possible.

```

**Constraints:**

- `1 <= n <= 500`
- `1 <= edges.length <= 104`
- `edges[i].length == 2`
- `1 <= ai, bi <= n`
- `ai != bi`
- There is at most one edge between any pair of vertices.
```java
class Solution {
    public int magnificentSets(int n, int[][] edges) {
        // 重點:  Notice that the given graph may be disconnected.
        List<Integer>[] adj = new List[n];
        Arrays.setAll(adj, k -> new ArrayList<>());
        for (int[] e : edges) {
            int a = e[0] - 1, b = e[1] - 1;
            adj[a].add(b);
            adj[b].add(a);
        }
        int[] d = new int[n]; // 每個區塊的最大深度
        int[] dist = new int[n]; // 記錄 BFS 遍歷時的深度
        for (int i = 0; i < n; i++) {
            Queue<Integer> q = new LinkedList<>();
            q.offer(i);
            Arrays.fill(dist, 0);
            dist[i] = 1;
            int mx = 1; // 記錄最大深度
            int root = i; // 記錄該連通塊內最小的節點
            while (!q.isEmpty()) {
                int a = q.poll();
                root = Math.min(root, a);
                for (int b : adj[a]) {
                    if (dist[b] == 0) {// 還沒被遍歷過
                        dist[b] = dist[a] + 1;
                        mx = Math.max(mx, dist[b]);
                        q.offer(b);
                    } else if (Math.abs(dist[b] - dist[a]) != 1) {// 超過range
                        return -1;
                    }
                }
            }
            d[root] = Math.max(d[root], mx);
        }

        return Arrays.stream(d).sum();// 正常[n,0,0...] 但如果不連通[n,m,0,k...]
    }
}
```

