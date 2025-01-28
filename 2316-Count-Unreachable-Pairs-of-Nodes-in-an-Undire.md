# 2316. Count Unreachable Pairs of Nodes in an Undirected Graph

Data structure: Graph
Difficulty: Medium

You are given an integer `n`. There is an **undirected** graph with `n` nodes, numbered from `0` to `n - 1`. You are given a 2D integer array `edges` where `edges[i] = [ai, bi]` denotes that there exists an **undirected** edge connecting nodes `ai` and `bi`.

Return *the **number of pairs** of different nodes that are **unreachable** from each other*.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/05/05/tc-3.png](https://assets.leetcode.com/uploads/2022/05/05/tc-3.png)

```
Input: n = 3, edges = [[0,1],[0,2],[1,2]]
Output: 0
Explanation: There are no pairs of nodes that are unreachable from each other. Therefore, we return 0.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/05/05/tc-2.png](https://assets.leetcode.com/uploads/2022/05/05/tc-2.png)

```
Input: n = 7, edges = [[0,2],[0,5],[2,4],[1,6],[5,4]]
Output: 14
Explanation: There are 14 pairs of nodes that are unreachable from each other:
[[0,1],[0,3],[0,6],[1,2],[1,3],[1,4],[1,5],[2,3],[2,6],[3,4],[3,5],[3,6],[4,6],[5,6]].
Therefore, we return 14.

```

**Constraints:**

- `1 <= n <= 105`
- `0 <= edges.length <= 2 * 105`
- `edges[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- There are no repeated edges.

```jsx
class Solution {
    public long countPairs(int n, int[][] edges) {
        List<List<Integer>> adj = new ArrayList<>();
        //adj matrix
        for(int i = 0 ; i < n ; i++)
            adj.add(new ArrayList<>()); 
        for(int i = 0 ; i < edges.length ; i++){
            adj.get(edges[i][0]).add(edges[i][1]); //(4.0)
            adj.get(edges[i][1]).add(edges[i][0]);//(0.-4) 用正負表示方向
        }
        //相連的 合併同list 
        boolean[] visited = new boolean[n];
        Queue<Integer> q = new ArrayDeque<>();
        List<Long> num = new ArrayList<>();

        for(int i=0; i< n; i++){
            q.offer(i);
            if(visited[i] == false){
                long count = 0;
                while(!q.isEmpty()){
                    int a = q.poll();
                    if(visited[a]) continue;
                    count++;
                    visited[a] = true;
                    for(int sub : adj.get(a)){
                        if(!visited[sub])q.offer(sub);
                    }
                }
                num.add(count);
            }
        }
        return calculateResult(num, n);
    }
    public long calculateResult(List<Long> num, int n){
        long total = 0;
        for(int i=1; i < num.size(); i++){
            total += num.get(i - 1)*(n - num.get(i-1)); 
            n -= num.get(i - 1);
        }
        return total;
    }
}
```