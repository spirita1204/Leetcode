# 2392. Build a Matrix With Conditions

Methods: DFS, Order Traversal
Data structure: Graph, Hash Table
Difficulty: Hard

Hard

Topics

Companies

Hint

You are given a **positive** integer `k`. You are also given:

- a 2D integer array `rowConditions` of size `n` where `rowConditions[i] = [abovei, belowi]`, and
- a 2D integer array `colConditions` of size `m` where `colConditions[i] = [lefti, righti]`.

The two arrays contain integers from `1` to `k`.

You have to build a `k x k` matrix that contains each of the numbers from `1` to `k` **exactly once**. The remaining cells should have the value `0`.

The matrix should also satisfy the following conditions:

- The number `abovei` should appear in a **row** that is strictly **above** the row at which the number `belowi` appears for all `i` from `0` to `n - 1`.
- The number `lefti` should appear in a **column** that is strictly **left** of the column at which the number `righti` appears for all `i` from `0` to `m - 1`.

Return ***any** matrix that satisfies the conditions*. If no answer exists, return an empty matrix.

**Example 1:**

![https://assets.leetcode.com/uploads/2022/07/06/gridosdrawio.png](https://assets.leetcode.com/uploads/2022/07/06/gridosdrawio.png)

```
Input: k = 3, rowConditions = [[1,2],[3,2]], colConditions = [[2,1],[3,2]]
Output: [[3,0,0],[0,0,1],[0,2,0]]
Explanation: The diagram above shows a valid example of a matrix that satisfies all the conditions.
The row conditions are the following:
- Number 1 is in row1, and number 2 is in row2, so 1 is above 2 in the matrix.
- Number 3 is in row0, and number 2 is in row2, so 3 is above 2 in the matrix.
The column conditions are the following:
- Number 2 is in column1, and number 1 is in column2, so 2 is left of 1 in the matrix.
- Number 3 is in column0, and number 2 is in column1, so 3 is left of 2 in the matrix.
Note that there may be multiple correct answers.

```

**Example 2:**

```
Input: k = 3, rowConditions = [[1,2],[2,3],[3,1],[2,3]], colConditions = [[2,1]]
Output: []
Explanation: From the first two conditions, 3 has to be below 1 but the third conditions needs 3 to be above 1 to be satisfied.
No matrix can satisfy all the conditions, so we return the empty matrix.

```

**Constraints:**

- `2 <= k <= 400`
- `1 <= rowConditions.length, colConditions.length <= 104`
- `rowConditions[i].length == colConditions[i].length == 2`
- `1 <= abovei, belowi, lefti, righti <= k`
- `abovei != belowi`
- `lefti != righti`

```java
class Solution {
    public int[][] buildMatrix(int k, int[][] rowConditions, int[][] colConditions) {
        List<Integer> rowSort = topoSort(rowConditions, k);// [3, 1, 2] -> [0,0]放3 [2,1]放1 [1,2]放2
        List<Integer> colSort = topoSort(colConditions, k);// [3, 2, 1] 根據座標放入
        // System.out.println(rowSort);
        // System.out.println(colSort);
        if (rowSort.isEmpty() || colSort.isEmpty())
            return new int[0][0];

        List<int[]> valuePosition = new ArrayList<>();
        for (int n = 0; n < k; n++) {// 產生最終圖
            valuePosition.add(new int[2]); // element -> [row_index, col_index]
        }
        for (int i = 0; i < rowSort.size(); i++) {
            valuePosition.get(rowSort.get(i) - 1)[0] = i;
        }
        for (int i = 0; i < colSort.size(); i++) {
            valuePosition.get(colSort.get(i) - 1)[1] = i;
        }
        int[][] res = new int[k][k];
        for (int value = 0; value < k; ++value) {
            int row = valuePosition.get(value)[0];
            int column = valuePosition.get(value)[1];
            res[row][column] = value + 1;
        }
        return res;
    }

    // if there will be cycle - return empty array,
    // in other case return 1d array as described above
    private List<Integer> topoSort(int[][] edges, int k) {// [[1,2],[3,2]] -> [3,1,2]
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int[] edge : edges) {// 建立有向圖
            graph.computeIfAbsent(edge[0], x -> new ArrayList<>()).add(edge[1]);
        }
        List<Integer> visited = new ArrayList<>();// 是否有走過
        List<Integer> res = new ArrayList<>();// 結果
        // List<Integer> cycle = new ArrayList<>();// 判斷是否有迴圈

        for(int i = 1; i <= k; i++) {// 1,2,3開始點 每點都要有
            if(dfs(i, graph, visited, res, new ArrayList<>())) {//代表有迴圈
                // 直接輸出空陣列
                return Collections.emptyList();
            } 
        }
        // 原本從子排到父 需反轉
        Collections.reverse(res);
        return res;
    }
    // postOrder 先做子節點 再做父節點
    // false 代表有迴圈
    // true 代表正常
    private boolean dfs(int i,  Map<Integer, List<Integer>> graph, List<Integer> visited,  List<Integer> res, List<Integer> cycle) {
        if(cycle.contains(i)) return true;
        if(visited.contains(i)) return false;  
        // 記錄走過
        visited.add(i);
        cycle.add(i);
        // 遍歷子節點
        List<Integer> childs = graph.get(i);
        if(childs != null) {
            for(int child: childs) {
                boolean isCycle = dfs(child, graph, visited, res, cycle);
                if(isCycle) return true;
            }
        }
        // 清空迴圈
        cycle.remove(Integer.valueOf(i));
        // 將最後塞入
        res.add(i);

        return false;
    }
}
```