# 1319. Number of Operations to Make Network Connected

Methods: DFS
Data structure: Graph
Difficulty: Medium

[Easy to understand Java implementation using find disconnected components concept - Number of Operations to Make Network Connected - LeetCode](https://leetcode.com/problems/number-of-operations-to-make-network-connected/solutions/1195926/easy-to-understand-java-implementation-using-find-disconnected-components-concept/?orderBy=most_votes)

There are `n` computers numbered from `0` to `n - 1` connected by ethernet cables `connections` forming a network where `connections[i] = [ai, bi]` represents a connection between computers `ai` and `bi`. Any computer can reach any other computer directly or indirectly through the network.

You are given an initial computer network `connections`. You can extract certain cables between two directly connected computers, and place them between any pair of disconnected computers to make them directly connected.

Return *the minimum number of times you need to do this in order to make all the computers connected*. If it is not possible, return `-1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/01/02/sample_1_1677.png](https://assets.leetcode.com/uploads/2020/01/02/sample_1_1677.png)

```
Input: n = 4, connections = [[0,1],[0,2],[1,2]]
Output: 1
Explanation: Remove cable between computer 1 and 2 and place between computers 1 and 3.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/01/02/sample_2_1677.png](https://assets.leetcode.com/uploads/2020/01/02/sample_2_1677.png)

```
Input: n = 6, connections = [[0,1],[0,2],[0,3],[1,2],[1,3]]
Output: 2

```

**Example 3:**

```
Input: n = 6, connections = [[0,1],[0,2],[0,3],[1,2]]
Output: -1
Explanation: There are not enough cables.

```

**Constraints:**

- `1 <= n <= 105`
- `1 <= connections.length <= min(n * (n - 1) / 2, 105)`
- `connections[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- There are no repeated connections.
- No two computers are connected by more than one cable.

```java
class Solution {
    public int makeConnected(int n, int[][] connections) {
        if(connections.length<n-1)
            return -1;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i=0;i<n;i++)
            adj.add(new ArrayList<>());
        for(int[] edge : connections){
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
        }
        
        boolean[] visited = new boolean[n];  
        int count = 0;

        for(int i=0;i<n;i++){
            if(!visited[i]){
                System.out.println("aa");
                count++;
                dfs(adj, i, visited);
            }
        }
        return count-1;
    }
    public void dfs(ArrayList<ArrayList<Integer>> adj, int node, boolean[] visited){
        if(visited[node])
            return;
        visited[node] = true;
        for(int i : adj.get(node)){
            dfs(adj, i, visited);
        }
    }
}
```