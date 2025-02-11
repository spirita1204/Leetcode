# 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance

Methods: DP, Shortest Path
Data structure: Graph
Difficulty: Medium

Medium

Topics

Companies

Hint

There are `n` cities numbered from `0` to `n-1`. Given the array `edges` where `edges[i] = [fromi, toi, weighti]` represents a bidirectional and weighted edge between cities `fromi` and `toi`, and given the integer `distanceThreshold`.

Return the city with the smallest number of cities that are reachable through some path and whose distance is **at most** `distanceThreshold`, If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities ***i*** and ***j*** is equal to the sum of the edges' weights along that path.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/01/16/find_the_city_01.png](https://assets.leetcode.com/uploads/2020/01/16/find_the_city_01.png)

```
Input: n = 4, edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4
Output: 3
Explanation:The figure above describes the graph.
The neighboring cities at a distanceThreshold = 4 for each city are:
City 0 -> [City 1, City 2]
City 1 -> [City 0, City 2, City 3]
City 2 -> [City 0, City 1, City 3]
City 3 -> [City 1, City 2]
Cities 0 and 3 have 2 neighboring cities at a distanceThreshold = 4, but we have to return city 3 since it has the greatest number.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/01/16/find_the_city_02.png](https://assets.leetcode.com/uploads/2020/01/16/find_the_city_02.png)

```
Input: n = 5, edges = [[0,1,2],[0,4,8],[1,2,3],[1,4,2],[2,3,1],[3,4,1]], distanceThreshold = 2
Output: 0
Explanation:The figure above describes the graph.
The neighboring cities at a distanceThreshold = 2 for each city are:
City 0 -> [City 1]
City 1 -> [City 0, City 4]
City 2 -> [City 3, City 4]
City 3 -> [City 2, City 4]
City 4 -> [City 1, City 2, City 3]
The city 0 has 1 neighboring city at a distanceThreshold = 2.

```

**Constraints:**

- `2 <= n <= 100`
- `1 <= edges.length <= n * (n - 1) / 2`
- `edges[i].length == 3`
- `0 <= fromi < toi < n`
- `1 <= weighti, distanceThreshold <= 10^4`
- All pairs `(fromi, toi)` are distinct.

```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        // https://hackmd.io/@konchin/shortest_path
        // Floyd-Warshall shortest path 
        int node = -1;
        int[][] dis = new int[n][n];
        // 距離10001代表到不了
        for (int[] row : dis)
            Arrays.fill(row, 10001);
        for(int[] edge: edges) {
            dis[edge[0]][edge[1]] = edge[2];
            dis[edge[1]][edge[0]] = edge[2];
        }
        // 建立最短路徑
        for(int k = 0; k < n; k++)
            for(int i = 0; i < n; i++)
                for(int j = 0; j < n; j++)
                    dis[i][j] = Math.min(dis[i][j], dis[i][k] + dis[k][j]);
        // 遍歷陣列 對每一節點
        int minCnt = Integer.MAX_VALUE;
        for(int i = 0; i < dis.length; i++) {
            int cnt = 0;
            for(int j = 0; j < dis.length; j++) {
                if(i != j && dis[i][j] <= distanceThreshold) 
                    cnt++;
            }
            if(cnt < minCnt) {
                minCnt = cnt;
                node = i;
            } 
            // 相同時 輸出最大數字cities
            else if(cnt == minCnt && node < i) {
                node = i;
            }
        }
        return node;
    }
}
```