# 802. Find Eventual Safe States

Methods: DFS
Data structure: Graph
Difficulty: Medium++

There is a directed graph of `n` nodes with each node labeled from `0` to `n - 1`. The graph is represented by a **0-indexed** 2D integer array `graph` where `graph[i]` is an integer array of nodes adjacent to node `i`, meaning there is an edge from node `i` to each node in `graph[i]`.

A node is a **terminal node** if there are no outgoing edges. A node is a **safe node** if every possible path starting from that node leads to a **terminal node** (or another safe node).

Return *an array containing all the **safe nodes** of the graph*. The answer should be sorted in **ascending** order.

**Example 1:**

![https://s3-lc-upload.s3.amazonaws.com/uploads/2018/03/17/picture1.png](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/03/17/picture1.png)

```
Input: graph = [[1,2],[2,3],[5],[0],[5],[],[]]
Output: [2,4,5,6]
Explanation: The given graph is shown above.
Nodes 5 and 6 are terminal nodes as there are no outgoing edges from either of them.
Every path starting at nodes 2, 4, 5, and 6 all lead to either node 5 or 6.
```

**Example 2:**

```
Input: graph = [[1,2,3,4],[1,2],[3,4],[0,4],[]]
Output: [4]
Explanation:
Only node 4 is a terminal node, and every path starting at node 4 leads to node 4.

```

**Constraints:**

- `n == graph.length`
- `1 <= n <= 104`
- `0 <= graph[i].length <= n`
- `0 <= graph[i][j] <= n - 1`
- `graph[i]` is sorted in a strictly increasing order.
- The graph may contain self-loops.
- The number of edges in the graph will be in the range `[1, 4 * 104]`.

DFS

```java
class Solution {
    public boolean dfs(List<List<Integer>> adj, int src, boolean[] vis, boolean[] recst) {
        //    0     1    2   3   4  5  6
        // [[1,2],[2,3],[5],[0],[5],[],[]]
        vis[src] = true;
        recst[src] = true;
        for (int x : adj.get(src)) {
            if (!vis[x] && dfs(adj, x, vis, recst)) {// 未訪問&& ..
                return true;// 表示圖中存在循
            } else if (recst[x]) {
                return true;// 表示圖中存在循
            }
        }
        recst[src] = false;// 該節點不屬於循環。
        return false;
    }

    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        List<List<Integer>> adj = new ArrayList<>();
        // build graph
        for (int i = 0; i < n; i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j < graph[i].length; j++) {
                list.add(graph[i][j]);
            }
            adj.add(list);
        }
        boolean[] vis = new boolean[n]; // VISITED
        boolean[] recst = new boolean[n];// 檢測是否存在循環。如果 recst[i] 為 true，則節點 i 不安全。
        for (int i = 0; i < n; i++) {// scan all node
            if (!vis[i]) {
                dfs(adj, i, vis, recst);
            }
        }
        List<Integer> ans = new ArrayList<>();
        for (int i = 0; i < recst.length; i++) {
            if (!recst[i]) {
                ans.add(i);
            }
        }
        return ans;
    }
}
```

DFS+Memo(state)

```sql
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        int[] state = new int[n]; // 0: 未訪問, 1: 不安全, 2: 安全
        List<Integer> result = new ArrayList<>();

        // 判斷節點是否安全
        for (int i = 0; i < n; i++) {
            if (dfs(graph, i, state)) {
                result.add(i);
            }
        }

        return result;
    }

    private boolean dfs(int[][] graph, int node, int[] state) {
        if (state[node] != 0) {
            // 如果該節點已經計算過，直接返回結果
            return state[node] == 2;
        }

        state[node] = 1; // 標記為不安全 (正在遞歸中)
        for (int neighbor : graph[node]) {
            if (!dfs(graph, neighbor, state)) {
                return false; // 如果鄰居不安全，該節點也不安全
            }
        }
        state[node] = 2; // 標記為安全
        return true;
    }
}

```