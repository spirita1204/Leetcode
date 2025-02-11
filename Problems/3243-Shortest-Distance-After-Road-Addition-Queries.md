# 3243. Shortest Distance After Road Addition Queries I

Methods: BFS
Data structure: Graph
Difficulty: Medium

You are given an integer `n` and a 2D integer array `queries`.

There are `n` cities numbered from `0` to `n - 1`. Initially, there is a **unidirectional** road from city `i` to city `i + 1` for all `0 <= i < n - 1`.

`queries[i] = [ui, vi]` represents the addition of a new **unidirectional** road from city `ui` to city `vi`. After each query, you need to find the **length** of the **shortest path** from city `0` to city `n - 1`.

Return an array `answer` where for each `i` in the range `[0, queries.length - 1]`, `answer[i]` is the *length of the shortest path* from city `0` to city `n - 1` after processing the **first** `i + 1` queries.

**Example 1:**

**Input:** n = 5, queries = [[2,4],[0,2],[0,4]]

**Output:** [3,2,1]

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/28/image8.jpg](https://assets.leetcode.com/uploads/2024/06/28/image8.jpg)

After the addition of the road from 2 to 4, the length of the shortest path from 0 to 4 is 3.

![https://assets.leetcode.com/uploads/2024/06/28/image9.jpg](https://assets.leetcode.com/uploads/2024/06/28/image9.jpg)

After the addition of the road from 0 to 2, the length of the shortest path from 0 to 4 is 2.

![https://assets.leetcode.com/uploads/2024/06/28/image10.jpg](https://assets.leetcode.com/uploads/2024/06/28/image10.jpg)

After the addition of the road from 0 to 4, the length of the shortest path from 0 to 4 is 1.

**Example 2:**

**Input:** n = 4, queries = [[0,3],[0,2]]

**Output:** [1,1]

**Explanation:**

![https://assets.leetcode.com/uploads/2024/06/28/image11.jpg](https://assets.leetcode.com/uploads/2024/06/28/image11.jpg)

After the addition of the road from 0 to 3, the length of the shortest path from 0 to 3 is 1.

![https://assets.leetcode.com/uploads/2024/06/28/image12.jpg](https://assets.leetcode.com/uploads/2024/06/28/image12.jpg)

After the addition of the road from 0 to 2, the length of the shortest path remains 1.

**Constraints:**

- `3 <= n <= 500`
- `1 <= queries.length <= 500`
- `queries[i].length == 2`
- `0 <= queries[i][0] < queries[i][1] < n`
- `1 < queries[i][1] - queries[i][0]`
- There are no repeated roads among the queries.

---

Maintain the graph and use an efficient shortest path algorithm after each update.

---

We use BFS/Dijkstra for each query.

---

Runtime **5.02%**

Memory **5.41%**

```java
class Solution {
    public int[] shortestDistanceAfterQueries(int n, int[][] queries) {
        List<List<Integer>> graph = new ArrayList<>();
        int[] res = new int[queries.length];
        int idx = 0;

        for(int i = 0; i< n; i++) 
            graph.add(i, new ArrayList<>());
        // 新串聯
        for(int[] edge : queries){
            int u = edge[0];
            int v = edge[1];
            graph.get(u).add(v);
            res[idx++] = bfs(graph, n) - 2;
        }
        return res;
    }

    private int bfs(List<List<Integer>> graph, int n) {
        Queue<Integer> q = new LinkedList<>(); 
        int cnt = 0;
        // purning
        boolean[] visited = new boolean[n];

        q.offer(0);
        while(!q.isEmpty()) {
            int size = q.size();
            cnt++;
            while(size-- > 0) {
                int node = q.poll();
                if(node == n) 
                    return cnt;
                visited[node] = true;
                List<Integer> next = graph.get(node);
                for(int nt: next) 
                    if(!visited[nt])
                        q.offer(nt);
                // 本身下一個
                q.offer(node + 1);
            }
        }
        return cnt;
    }
}
```

---

修正版本 變快

```jsx

```