# 3607. Power Grid Maintenance  

  Data Structure: Union Find </br> Difficulty: Medium </br> </br>You are given an integer `c` representing `c` power stations, each with a unique identifier `id` from 1 to `c` (1‑based indexing).

These stations are interconnected via `n` **bidirectional** cables, represented by a 2D array `connections`, where each element `connections[i] = [ui, vi]` indicates a connection between station `ui` and station `vi`. Stations that are directly or indirectly connected form a **power grid**.

Initially, **all** stations are online (operational).

You are also given a 2D array `queries`, where each query is one of the following *two* types:

- `[1, x]`: A maintenance check is requested for station `x`. If station `x` is online, it resolves the check by itself. If station `x` is offline, the check is resolved by the operational station with the smallest `id` in the same **power grid** as `x`. If **no** **operational** station *exists* in that grid, return -1.
- `[2, x]`: Station `x` goes offline (i.e., it becomes non-operational).
Return an array of integers representing the results of each query of type `[1, x]` in the **order** they appear.

**Note:** The power grid preserves its structure; an offline (non‑operational) node remains part of its grid and taking it offline does not alter connectivity.

**Example 1:**

**Input:** c = 5, connections = [[1,2],[2,3],[3,4],[4,5]], queries = [[1,3],[2,1],[1,1],[2,2],[1,2]]

**Output:** [3,2,3]

**Explanation:**

![Image](https://assets.leetcode.com/uploads/2025/04/15/powergrid.jpg)

- Initially, all stations `{1, 2, 3, 4, 5}` are online and form a single power grid.
- Query `[1,3]`: Station 3 is online, so the maintenance check is resolved by station 3.
- Query `[2,1]`: Station 1 goes offline. The remaining online stations are `{2, 3, 4, 5}`.
- Query `[1,1]`: Station 1 is offline, so the check is resolved by the operational station with the smallest `id` among `{2, 3, 4, 5}`, which is station 2.
- Query `[2,2]`: Station 2 goes offline. The remaining online stations are `{3, 4, 5}`.
- Query `[1,2]`: Station 2 is offline, so the check is resolved by the operational station with the smallest `id` among `{3, 4, 5}`, which is station 3.
**Example 2:**

**Input:** c = 3, connections = [], queries = [[1,1],[2,1],[1,1]]

**Output:** [1,-1]

**Explanation:**

- There are no connections, so each station is its own isolated grid.
- Query `[1,1]`: Station 1 is online in its isolated grid, so the maintenance check is resolved by station 1.
- Query `[2,1]`: Station 1 goes offline.
- Query `[1,1]`: Station 1 is offline and there are no other stations in its grid, so the result is -1.
**Constraints:**

- `1 <= c <= 105`
- `0 <= n == connections.length <= min(105, c * (c - 1) / 2)`
- `connections[i].length == 2`
- `1 <= ui, vi <= c`
- `ui != vi`
- `1 <= queries.length <= 2 * 105`
- `queries[i].length == 2`
- `queries[i][0]` is either 1 or 2.
- `1 <= queries[i][1] <= c`
```java
class Solution {
    int[] parent, size;
    Map<Integer, PriorityQueue<Integer>> mp = new HashMap<>();

    int findParent(int node) {
        if (parent[node] == node) return node;
        return parent[node] = findParent(parent[node]);
    }

    void Union(int u, int v) {
        int up = findParent(u);
        int vp = findParent(v);

        if (up == vp) return;

        if (size[up] > size[vp]) {
            size[up] += size[vp];
            parent[vp] = up;
            PriorityQueue<Integer> pqV = mp.get(vp);
            PriorityQueue<Integer> pqU = mp.get(up);
            while (!pqV.isEmpty()) pqU.offer(pqV.poll());
        } else {
            size[vp] += size[up];
            parent[up] = vp;
            PriorityQueue<Integer> pqU = mp.get(up);
            PriorityQueue<Integer> pqV = mp.get(vp);
            while (!pqU.isEmpty()) pqV.offer(pqU.poll());
        }
    }

    public int[] processQueries(int c, int[][] connections, int[][] queries) {
        parent = new int[c];
        size = new int[c];
        boolean[] offline = new boolean[c];

        for (int i = 0; i < c; i++) {
            parent[i] = i;
            size[i] = 1;
            PriorityQueue<Integer> pq = new PriorityQueue<>();
            pq.offer(i);
            mp.put(i, pq);
        }

        for (int[] conn : connections) {
            int u = conn[0] - 1, v = conn[1] - 1;
            Union(u, v);
        }

        List<Integer> ans = new ArrayList<>();

        for (int[] q : queries) {
            int type = q[0];
            int node = q[1] - 1;

            if (type == 1) {
                if (!offline[node]) {
                    ans.add(node + 1);
                    continue;
                }
                int par = findParent(node);
                PriorityQueue<Integer> pq = mp.get(par);
                while (!pq.isEmpty() && offline[pq.peek()]) pq.poll();
                ans.add(pq.isEmpty() ? -1 : pq.peek() + 1);
            } else {
                offline[node] = true;
            }
        }

        return ans.stream().mapToInt(i -> i).toArray();
    }
}
```

