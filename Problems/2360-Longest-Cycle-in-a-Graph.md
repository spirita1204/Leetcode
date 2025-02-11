# 2360. Longest Cycle in a Graph

Methods: BFS
Difficulty: Hard

[https://www.youtube.com/watch?v=_eeiFV137pw&ab_channel=HuifengGuan](https://www.youtube.com/watch?v=_eeiFV137pw&ab_channel=HuifengGuan)

You are given a **directed** graph of `n` nodes numbered from `0` to `n - 1`, where each node has **at most one** outgoing edge.

The graph is represented with a given **0-indexed** array `edges` of size `n`, indicating that there is a directed edge from node `i` to node `edges[i]`. If there is no outgoing edge from node `i`, then `edges[i] == -1`.

Return *the length of the **longest** cycle in the graph*. If no cycle exists, return `-1`.

A cycle is a path that starts and ends at the **same** node.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/06/08/graph4drawio-5.png](https://assets.leetcode.com/uploads/2022/06/08/graph4drawio-5.png)

```
Input: edges = [3,3,4,2,3]
Output: 3
Explanation: The longest cycle in the graph is the cycle: 2 -> 4 -> 3 -> 2.
The length of this cycle is 3, so 3 is returned.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-1.png](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-1.png)

```
Input: edges = [2,-1,3,1]
Output: -1
Explanation: There are no cycles in this graph.

```

**Constraints:**

- `n == edges.length`
- `2 <= n <= 105`
- `1 <= edges[i] < n`
- `edges[i] != i`

```html
class Solution {
    public int longestCycle(int[] edges) {
        //判斷有無indegree 然後刪除完 遍歷最大的圈
        int n = edges.length;
        int[] inDegree =  new int[n];
        //計算 入邊數
        for(int i = 0; i < n ; i++){
            if(edges[i] != -1){ 
                inDegree[edges[i]]++;
            }
        }
        Queue<Integer> q = new ArrayDeque<>();
        //入邊數為0的點
        boolean[] visited = new boolean[n]; 
        for(int i=0;i<n;i++){
            if(inDegree[i] == 0){
                visited[i] = true;
                q.offer(i);
            }
        }
        //從入邊數為0開始砍
        while(!q.isEmpty()){
            int sub = q.poll(); 
            int adj = edges[sub]; //與sub相鄰的 
            if(adj == -1) continue;
            inDegree[adj]--;//入 將會減少一
            if(inDegree[adj] == 0){
                q.offer(adj);
                visited[adj] = true;
            }
        }
        //沒訪問過的 都在環上面
        int res = -1;
        for(int i = 0;i< n;i++){
            if(visited[i]) continue;
            int j = i;
            int counter = 1;
            visited[j] = true;
            while(edges[j] != -1 && visited[edges[j]] == false){
                counter++;
                j = edges[j];
                visited[j] = true;
            }
            res = Math.max(res, counter);
        }
        return (res == 1) ? -1 : res;
    }
}
```