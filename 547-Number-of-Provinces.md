# 547. Number of Provinces

Data structure: Graph
Difficulty: Medium

**Medium**

7.4K

285

Companies

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return *the total number of **provinces***.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

```
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3

```

**Constraints:**

- `1 <= n <= 200`
- `n == isConnected.length`
- `n == isConnected[i].length`
- `isConnected[i][j]` is `1` or `0`.
- `isConnected[i][i] == 1`
- `isConnected[i][j] == isConnected[j][i]`

Accepted

**613.5K**

Submissions

**961.5K**

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int provinces = 0;
        int n = isConnected.length;
        //先轉為相鄰矩陣
        List<List<Integer>> graph = new ArrayList<>();
        for(int i = 0; i< n; i++)
            graph.add(new ArrayList<>());
        for(int i = 0;i < n; i++){
            for(int j = 0;j< n; j++){
                if(isConnected[i][j] == 1) graph.get(i).add(j);    
            }
            
        }
        boolean[] visited = new boolean[n];  
        //遍歷所有點 看是否有去過
        for(int i= 0; i< n; i++){
            if(!visited[i]){
                dfs(graph, i, visited);
                provinces++;
            }
        }
        return provinces;
    }
    public void dfs(List<List<Integer>> graph, int node, boolean[] visited){
        //當走訪有去過 就return
        if(visited[node]) return;
        visited[node] = true;
        //遍歷所有相鄰
        for(int i : graph.get(node)){
            dfs(graph, i, visited);
        }
    }
}
```