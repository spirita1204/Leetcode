# 797. All Paths From Source to Target

Methods: DFS
Difficulty: Medium

**Medium**

6.4K

133

Companies

Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg](https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg)

```
Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/09/28/all_2.jpg](https://assets.leetcode.com/uploads/2020/09/28/all_2.jpg)

```
Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]

```

**Constraints:**

- `n == graph.length`
- `2 <= n <= 15`
- `0 <= graph[i][j] < n`
- `graph[i][j] != i` (i.e., there will be no self-loops).
- All the elements of `graph[i]` are **unique**.
- The input graph is **guaranteed** to be a **DAG**.

```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        int row = graph.length;
        // 相鄰矩陣
        List<List<Integer>> adj = new ArrayList<>();
        // 輸出
        List<List<Integer>> res = new ArrayList<>();

        for(int i = 0; i< row; i++){
            adj.add(new ArrayList<>());
        }
        for(int i = 0; i< row; i++){
            for(int j = 0; j< graph[i].length; j++){
                adj.get(i).add(graph[i][j]);
            }
        }
        dfs(graph, adj, new ArrayList<Integer>(), res, 0);

        return res;
    }
    public void dfs(int[][] graph, List<List<Integer>> adj, List<Integer> sub, List<List<Integer>> res, int i){
        sub.add(i);

        if(i == graph.length - 1){// 當到達終點
            res.add(new ArrayList<>(sub));
            return;
        }

        for(int e: adj.get(i)){
            dfs(graph, adj, sub, res, e);
            //刪除最後一位元
            sub.remove(sub.size()- 1);
        }  
    }
}
```