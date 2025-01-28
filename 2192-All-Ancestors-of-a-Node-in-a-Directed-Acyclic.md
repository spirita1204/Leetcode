# 2192. All Ancestors of a Node in a Directed Acyclic Graph

Methods: DFS
Data structure: Graph
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a positive integer `n` representing the number of nodes of a **Directed Acyclic Graph** (DAG). The nodes are numbered from `0` to `n - 1` (**inclusive**).

You are also given a 2D integer array `edges`, where `edges[i] = [fromi, toi]` denotes that there is a **unidirectional** edge from `fromi` to `toi` in the graph.

Return *a list* `answer`*, where* `answer[i]` *is the **list of ancestors** of the* `ith` *node, sorted in **ascending order***.

A node `u` is an **ancestor** of another node `v` if `u` can reach `v` via a set of edges.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/12/12/e1.png](https://assets.leetcode.com/uploads/2019/12/12/e1.png)

```
Input: n = 8, edgeList = [[0,3],[0,4],[1,3],[2,4],[2,7],[3,5],[3,6],[3,7],[4,6]]
Output: [[],[],[],[0,1],[0,2],[0,1,3],[0,1,2,3,4],[0,1,2,3]]
Explanation:
The above diagram represents the input graph.
- Nodes 0, 1, and 2 do not have any ancestors.
- Node 3 has two ancestors 0 and 1.
- Node 4 has two ancestors 0 and 2.
- Node 5 has three ancestors 0, 1, and 3.
- Node 6 has five ancestors 0, 1, 2, 3, and 4.
- Node 7 has four ancestors 0, 1, 2, and 3.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2019/12/12/e2.png](https://assets.leetcode.com/uploads/2019/12/12/e2.png)

```
Input: n = 5, edgeList = [[0,1],[0,2],[0,3],[0,4],[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Output: [[],[0],[0,1],[0,1,2],[0,1,2,3]]
Explanation:
The above diagram represents the input graph.
- Node 0 does not have any ancestor.
- Node 1 has one ancestor 0.
- Node 2 has two ancestors 0 and 1.
- Node 3 has three ancestors 0, 1, and 2.
- Node 4 has four ancestors 0, 1, 2, and 3.

```

**Constraints:**

- `1 <= n <= 1000`
- `0 <= edges.length <= min(2000, n * (n - 1) / 2)`
- `edges[i].length == 2`
- `0 <= fromi, toi <= n - 1`
- `fromi != toi`
- There are no duplicate edges.
- The graph is **directed** and **acyclic**.

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> getAncestors(int n, int[][] edges) {
        List<List<Integer>> adj = new ArrayList<>();
        // 產生相鄰矩陣
        for(int i = 0; i < n; i++) 
            adj.add(new ArrayList<>());
        // 串連
        for(int i = 0; i < edges.length; i++) // 將指標反向 dfs下去 
            adj.get(edges[i][1]).add(edges[i][0]);
        // DFS
        for(int i = 0; i < n; i++) {
            List<Integer> sub = new ArrayList<>();
            dfs(adj, sub, i);
            Collections.sort(sub);
            res.add(new ArrayList<>(sub));
        }
        return res;
    }

    private void dfs (List<List<Integer>> adj, List<Integer> sub, int i) {
        List<Integer> e = adj.get(i);
        if(e.size() == 0) return;

        for(int j = 0; j < e.size(); j++) {
            if(!sub.contains(e.get(j))) {// 避免重複遍歷
                sub.add(e.get(j));
            } else continue;// purning
            dfs(adj, sub, e.get(j));
        }
    }
}
```