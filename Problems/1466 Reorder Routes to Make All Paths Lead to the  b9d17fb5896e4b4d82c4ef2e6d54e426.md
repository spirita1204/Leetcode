# 1466. Reorder Routes to Make All Paths Lead to the City Zero

Data structure: Graph
Difficulty: Medium

**Medium**

2.3K

58

Companies

There are `n` cities numbered from `0` to `n - 1` and `n - 1` roads such that there is only one way to travel between two different cities (this network form a tree). Last year, The ministry of transport decided to orient the roads in one direction because they are too narrow.

Roads are represented by `connections` where `connections[i] = [ai, bi]` represents a road from city `ai` to city `bi`.

This year, there will be a big event in the capital (city `0`), and many people want to travel to this city.

Your task consists of reorienting some roads such that each city can visit the city `0`. Return the **minimum** number of edges changed.

It's **guaranteed** that each city can reach city `0` after reorder.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/05/13/sample_1_1819.png](https://assets.leetcode.com/uploads/2020/05/13/sample_1_1819.png)

```
Input: n = 6, connections = [[0,1],[1,3],[2,3],[4,0],[4,5]]
Output: 3
Explanation:Change the direction of edges show in red such that each node can reach the node 0 (capital).

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/05/13/sample_2_1819.png](https://assets.leetcode.com/uploads/2020/05/13/sample_2_1819.png)

```
Input: n = 5, connections = [[1,0],[1,2],[3,2],[3,4]]
Output: 2
Explanation:Change the direction of edges show in red such that each node can reach the node 0 (capital).

```

**Example 3:**

```
Input: n = 3, connections = [[1,0],[2,0]]
Output: 0

```

**Constraints:**

- `2 <= n <= 5 * 104`
- `connections.length == n - 1`
- `connections[i].length == 2`
- `0 <= ai, bi <= n - 1`
- `ai != bi`

```java
class Solution {
    public int minReorder(int n, int[][] connections) {
        int totalChange = 0;
        List<List<Integer>> adj = new ArrayList<>();
        boolean[] visited = new boolean[n];

        for(int i = 0 ; i < n ; i++)
            adj.add(new ArrayList<>()); 
        for(int i = 0 ; i < connections.length ; i++){
            adj.get(connections[i][0]).add(connections[i][1]); //(4.0)
            adj.get(connections[i][1]).add(-connections[i][0]);//(0.-4) 用正負表示方向
        }

        Queue<Integer> q = new ArrayDeque<>();
        q.offer(0);

        while(!q.isEmpty()){
            int now = q.poll();
            visited[Math.abs(now)] = true;
            
            for(int i : adj.get(Math.abs(now))){
                if(!visited[Math.abs(i)]){
                    q.add(i);
                    if(i > 0)
                        totalChange++;
                }
            }
        }
        return totalChange;
    }
}
```