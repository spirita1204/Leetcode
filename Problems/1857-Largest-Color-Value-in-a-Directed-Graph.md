# 1857. Largest Color Value in a Directed Graph  

  Data Structure: Graph </br> Difficulty: Hard </br> </br>There is a **directed graph** of `n` colored nodes and `m` edges. The nodes are numbered from `0` to `n - 1`.

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

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/1d06e5b4-aef7-4039-9d1e-324b0aa4cfcd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663R3B637Y%2F20250526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250526T155922Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEID%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCsjTrN9Pmh1O%2Bzw7zenCnz5RC%2BZXbVVu2SxNg3loOOOgIhAJxKreCahN5HDkR0SqnLrqtNe9ijy1Xzbzno8y21uUULKv8DCEkQABoMNjM3NDIzMTgzODA1IgzkdC72grsEZnSVZncq3APkwnIwVa6YgHrHzSicvuMisOMgEoauQm2h6Kd7LYeVsBg6%2Bx%2FB%2BMvUEvOSe7ilWcLGqCeW87b8wioAYTUoSLjANgHE2N36aUDj02%2Bcy8pKvx3K0uI2deJtNDkmgvx5eDPxCS0XrkPqXeB5NYkscbcuU%2BscriDfhL8%2BcQB5o6y3xiXyzUrhZsmFDFnR3TpkWeSRBs6n1VsrSi70Mub0QN%2BO0s4decFVGPNQ0KQNIWvOz0kHTHxL78oNnrPuUBTWMJqsBzXhu%2Fv0D04vu96vnOGhgLP7EqGZrwexzW2XXh1bmPE7am4JDsJnMZ9HYOmuaEjHxophrFAdunhRHEd0sij5E79llJ7PEwDJF5JH7RMkqANbQ8GVMKV7V2d7dIcjkIQmuzBwoUqEAHB21V0VfzjWzW5ZfefwERu9DHkyeMnWwWX5QMpu6G7ufRFvyCEDEzu3XedmwO1FHJc%2BCwGakSEMJE6F6o1rB5NwtJFbjuEw%2BDvXKJd8NkvRj9ZE1DjvJ6vQ8r1hP5%2FKZPmjpxqbVkwtdDL6BWnGJOqtf9F%2Bl0pv%2FuWKuPH0BTFSF%2BhN1tacR43jmm2fmcFNzuCTIoe%2Bn2NhKuAIFgeyjywh%2FP0O1NEnM49YLlk39kpEtzwxGTCEk9LBBjqkAXZdNPoqc5RQ47ls%2FuChYvD6xD1Vhc3LIR%2BBaUSPXvW%2BTZT2Jv8CLr9q3Gn5pOa0Lslj%2Fqco75M13E9uEF9K5zdRwC4LBP895twSqoS%2FN3%2BJbqxMOmIqvIzchzx4fa3lqfwfy2dJMMHAQVXPB3R1224gKSXO7NIIx0vzLXiXP1vULYoJCjUqRlQV%2FPdtmmQAX38hx88r96mM%2BbWs%2BCbu86CCXg9Y&X-Amz-Signature=9a25450cc6f5f5c843da1dee1287e4858bbfc9ba262c6da705ab288ca0aaa5cf&X-Amz-SignedHeaders=host&x-id=GetObject)

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
        //1. Build the Graph and Indegree array
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        int n = colors.length();//節點總數
        int[] indegree = new int[n];// 入 點個數陣列
        char[] color = colors.toCharArray(); 
        //建立各點物件
        for(int i = 0; i< n; i++) graph.add(i,new ArrayList<>());

        for(int[] edge : edges){
            int u = edge[0];
            int v = edge[1];
            indegree[v]++;
            graph.get(u).add(v);
        }
        //2. color count map. map[i][j] is the maximum count of j-th color from the ancester nodes to node i
        int[][] map = new int[n][26]; 
        //3.Khans Algorithm ( Iterative Topological Sort)
        Queue<Integer> que = new ArrayDeque<>();
        for(int i = 0; i< n; i++){
            if(indegree[i] == 0){//代表leaf
                que.add(i);
                map[i][color[i]-'a'] = 1;//當前顏色註記
            }
        }
        
        int res = 0;
        int seen = 0;//紀錄是否有走過所有節點
        
        while(!que.isEmpty()){
            int node = que.poll();
            seen++;
            
            int max = getMax(map[node]);
            res = Math.max(res,max);
            
            for(int nbr: graph.get(node)){//便歷相鄰
                // update the map of next node
                for(int i=0;i<26;i++){
                    map[nbr][i] = Math.max(map[nbr][i], map[node][i] + ((color[nbr]-'a' == i) ? 1 : 0));
                                                     //上一入節點 全值 + (當前顏色)
                }
                indegree[nbr]--;//刪除原本node節點 以nbr為leaf
                if(indegree[nbr]==0) que.offer(nbr);// 將leaf再次丟入queue
            }
        }
        //有cycle
        return seen == n ? res : -1;
    }
    //從26個字母當中找到最多的字母
    private int getMax(int[] num){
        int max = num[0];
        for(int n:num){
            max = Math.max(n,max);
        }
        return max;
    }
}
```

