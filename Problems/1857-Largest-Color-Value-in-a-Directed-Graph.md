# 1857. Largest Color Value in a Directed Graph  

  Methods: Topological Sort </br> Data Structure: Graph </br> Difficulty: Hard </br> </br>There is a **directed graph** of `n` colored nodes and `m` edges. The nodes are numbered from `0` to `n - 1`.

You are given a string `colors` where `colors[i]` is a lowercase English letter representing the **color** of the `ith` node in this graph (**0-indexed**). You are also given a 2D array `edges` where `edges[j] = [aj, bj]` indicates that there is a **directed edge** from node `aj` to node `bj`.

A valid **path** in the graph is a sequence of nodes `x1 -> x2 -> x3 -> ... -> xk` such that there is a directed edge from `xi` to `xi+1` for every `1 <= i < k`. The **color value** of the path is the number of nodes that are colored the **most frequently** occurring color along that path.

Return *the ****largest color value**** of any valid path in the given graph, or *`-1`* if the graph contains a cycle*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/04/21/leet1.png)

```plain text
Input: colors = "abaca", edges = [[0,1],[0,2],[2,3],[3,4]]
Output: 3
Explanation: The path 0 -> 2 -> 3 -> 4 contains 3 nodes that are colored"a" (red in the above image).
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/04/21/leet2.png)

```plain text
Input: colors = "a", edges = [[0,0]]
Output: -1
Explanation: There is a cycle from 0 to 0.
```

**Constraints:**

- `n == colors.length`
- `m == edges.length`
- `1 <= n <= 105`
- `0 <= m <= 105`
- `colors` consists of lowercase English letters.
- `0 <= aj, bj < n`
觀念 拆解成26子等分去思考 找單鏈 該顏色最多 > 最後在取26個中最大

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/1d06e5b4-aef7-4039-9d1e-324b0aa4cfcd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZOSCWH7S%2F20250530%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250530T123243Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjENz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIQCgnOVRx4f4UUzn07yqfWuZUPoAQkcdx9dQHezSYtPuUAIfD8r79ZFGy4elWA0A5dhco7m9pxht%2B3nC3bM0gEDARSqIBAil%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM1D5Sx6WNAipPbgHgKtwDJnQpJIZYK6WI%2F%2B5xCbd4hN0FC9GujXF74ZurKq7PZDUVWp7R%2B5cpRuw6xjPkufsDVMKsLzhh4cCYrQBrA%2FqbJ5FoUauybsU%2B2j81QxKj%2FHNzHuQ7Ol7lo3VxpX2G6S8bdUqas2oq0jLHSVrj46%2FPVZwuar%2BqU08LEHtMsFpdXdQ1gt475NjW95fuGtR60iKBcmuKVa%2FvlPPPRU8I2zCzI%2FOXUNeDJ7cKQbKelHJQl0gC3zhAmS3p%2BtjbjKBCah8J5wtt9oM7CdbYFmc1B2SCoQSWTyX9VXPHR7TI1Cl2BUMK9emdRJkcs%2Bv3eGyh6EEmb5vCBu7MXyXZvSz%2BqIof2%2BIPnxYdaICycPFidAJJV1Xp5U8c8cH1MhNHkt0PJRQiL%2BKcTqj1Pw5cFyBEfcnA3o0F3CXI4vcdIh45bzXckSCtwFY7ORs8TmT%2BVIz2GEcOmawG%2FKKtNpaPZEKRwa%2BGIuVaSU2z2e%2FN2wszzlB%2BSEWJXffwFYSE9VChHJph5tCoJfsS4JKLdfoiXI1tGlbr4E%2FEdP9elUyK4Wy67zNatBtw8gLIoxBRjGTSNUvg9suxmVzAjqyQX69yuqTXRDZPoH%2BuIsmZ5V4oCsGeXMBuOJTHLsh%2Fl35fd%2Bw8mW0w%2BrHmwQY6pgEN1na%2FKCZ32tXipnCswP28rvydCqjSqDR7zwjyUpc6A5mpQ%2BLqw9ItMcmMTFOnUmAzDfcDFwoPa9YWgi4J5MMtBSL0ZxZ3vZa8z%2BuKfoD0l%2Fahn6ZYszDOotlgWuvFm8qiSl9WXKqTOQAD4nWeRXqGAFGHM4dfVyM3z0lvl1GYPFH0PKAJYmh%2B38KR0taJHda2aYrLPKWoX6SSM2a8kI%2FfPk%2B2vmmB&X-Amz-Signature=b36c8c862b0b7dba26aac0aa249385c9adcf2bfece304a7abd05f6eaeb94360d&X-Amz-SignedHeaders=host&x-id=GetObject)

# **Topological Sort - Kahn's algorithm**

透過 topological sort 檢查圖中是否存在 cycle ，其步驟為：

1. 計算所有點的 in-degree (進入該點的邊數量）。
1. 將 in-degree 為 0 的點放入 queue 。
1. 從 queue 中拿出頂點，並執行以下步驟
1. 重複步驟 3 直到 queue 為空。
1. 檢查 dequeue 的數量是否等於節點總數 （如果存在 cycle 的話，cycle 路徑上的節點 in-degree 是永遠都無法歸零的）
```java
class Solution {
    public int largestPathValue(String colors, int[][] edges) {
        // 1. Build the Graph and Indegree array
        List<List<Integer>> graph = new ArrayList<>();
        int n = colors.length();// 節點總數
        int[] indegree = new int[n];// 入 點個數陣列
        char[] color = colors.toCharArray();
        // 建立各點物件
        for (int i = 0; i < n; i++)
            graph.add(i, new ArrayList<>());

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            indegree[v]++;
            graph.get(u).add(v);
        }
        // 2. 
        int[][] map = new int[n][26];
        // 3. Topological Sort
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {// 代表leaf
                q.offer(i);
                map[i][color[i] - 'a'] = 1;
            }
        }

        int res = 0;
        int seen = 0;// 紀錄是否有走過所有節點

        while (!q.isEmpty()) {
            int node = q.poll();
            seen++;

            int max = getMax(map[node]);
            res = Math.max(res, max);

            for (int nbr : graph.get(node)) {// 遍歷相鄰
                // update the map of next node
                for (int i = 0; i < 26; i++) {
                    map[nbr][i] = Math.max(map[nbr][i], map[node][i] + ((color[nbr] - 'a' == i) ? 1 : 0));
                    // 上一入節點 全值 + (當前顏色)
                }
                indegree[nbr]--;// 刪除原本node節點 以nbr為leaf
                if (indegree[nbr] == 0)
                    q.offer(nbr);// 將leaf再次丟入Queue
            }
        }
        // 有cycle
        return seen == n ? res : -1;
    }

    // 從26個字母當中找到最多的字母
    private int getMax(int[] num) {
        int max = num[0];
        for (int n : num) {
            max = Math.max(n, max);
        }
        return max;
    }
}
```

