# 743. Network Delay Time

Methods: DP, Shortest Path
Data structure: Graph
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return *the **minimum** time it takes for all the* `n` *nodes to receive the signal*. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png](https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png)

```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2

```

**Example 2:**

```
Input: times = [[1,2,1]], n = 2, k = 1
Output: 1

```

**Example 3:**

```
Input: times = [[1,2,1]], n = 2, k = 2
Output: -1

```

**Constraints:**

- `1 <= k <= n <= 100`
- `1 <= times.length <= 6000`
- `times[i].length == 3`
- `1 <= ui, vi <= n`
- `ui != vi`
- `0 <= wi <= 100`
- All the pairs `(ui, vi)` are **unique**. (i.e., no multiple edges.)

```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        // https://hackmd.io/@konchin/shortest_path
        // Floyd-Warshall shortest path 
        int[][] dis = new int[n][n];
        // 距離6000*100+ 1代表到不了
        for (int[] row : dis)
            Arrays.fill(row, 600001);
        for(int[] time: times)// 單向
            dis[time[0] - 1][time[1] - 1] = time[2];

        // 建立最短路徑
        for(int r = 0; r < n; r++)
            for(int i = 0; i < n; i++)
                for(int j = 0; j < n; j++)
                    dis[i][j] = Math.min(dis[i][j], dis[i][r] + dis[r][j]);
        // 取出從自己開始到其他人陣列
        int[] startToOther = dis[k - 1];
        int max = 0;
        for(int i = 0 ; i< startToOther.length; i++) {
            // 不用跟自己比
            if(i != k - 1) {
                if(startToOther[i] > 600000)
                    return -1;
                else max = Math.max(max, startToOther[i]);
            }
        }
        return max;
    }
}
```