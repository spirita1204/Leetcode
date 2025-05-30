# 2359. Find Closest Node to Given Two Nodes  

  Methods: BFS </br> Data Structure: Queue </br> Difficulty: Medium </br> </br>You are given a **directed** graph of `n` nodes numbered from `0` to `n - 1`, where each node has **at most one** outgoing edge.

The graph is represented with a given **0-indexed** array `edges` of size `n`, indicating that there is a directed edge from node `i` to node `edges[i]`. If there is no outgoing edge from `i`, then `edges[i] == -1`. 

You are also given two integers `node1` and `node2`.

Return *the ****index**** of the node that can be reached from both *`node1`* and *`node2`*, such that the ****maximum**** between the distance from *`node1`* to that node, and from *`node2`* to that node is ****minimized***. If there are multiple answers, return the node with the **smallest** index, and if no possible answer exists, return `-1`.

Note that `edges` may contain cycles.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-2.png)

```plain text
Input: edges = [2,2,3,-1], node1 = 0, node2 = 1
Output: 2
Explanation: The distance from node 0 to node 2 is 1, and the distance from node 1 to node 2 is 1.
The maximum of those two distances is 1. It can be proven that we cannot get a node with a smaller maximum distance than 1, so we return node 2.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-4.png)

```plain text
Input: edges = [1,2,-1], node1 = 0, node2 = 2
Output: 2
Explanation: The distance from node 0 to node 2 is 2, and the distance from node 2 to itself is 0.
The maximum of those two distances is 2. It can be proven that we cannot get a node with a smaller maximum distance than 2, so we return node 2.
```

**Constraints:**

- `n == edges.length`
- `2 <= n <= 105`
- `1 <= edges[i] < n`
- `edges[i] != i`
- `0 <= node1, node2 < n`
```java
class Solution {
    public int closestMeetingNode(int[] edges, int node1, int node2) {//注意cycle 和 unreached = -1
        int min = Integer.MAX_VALUE;// 比較所有最大
        int len = edges.length;

        int[] node1Dis = new int[len];// node1到所有點的距離 比較同i之最大 各路再取最小
        int[] node2Dis = new int[len];

        bfs(edges, node1, node1Dis);
        bfs(edges, node2, node2Dis);

        int res = -1;
        for (int i = 0; i < len; i++) {
            int temp = (node1Dis[i] == 0 || node2Dis[i] == 0) 
                ? Integer.MAX_VALUE // 無限大=>到不了
                : Math.max(node1Dis[i], node2Dis[i]);
                
            if (temp < min) {
                min = temp;
                res = i;
            }
        }

        return res;
    }

    public void bfs(int[] edges, int node, int[] nodeDis) {
        // BFS
        Queue<Integer> q = new LinkedList<>();
        q.offer(node);
        nodeDis[node] = -2;// 自己只到自己 設為-2
        int dis = 0;
        boolean[] vis = new boolean[edges.length];//避免cycle ex:[4,4,4,5,1,2,2]

        while (!q.isEmpty()) {
            int n = q.poll();
            if (edges[n] != -1 && vis[edges[n]] != true) {
                dis++;
                nodeDis[edges[n]] = dis;
                vis[n] = true;
                q.offer(edges[n]);
            }
        }
    }
}
```

