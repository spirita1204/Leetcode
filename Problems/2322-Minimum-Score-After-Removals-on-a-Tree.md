# 2322. Minimum Score After Removals on a Tree  

  Methods: DFS,Bitwise </br> Difficulty: Hard </br> </br>There is an undirected connected tree with `n` nodes labeled from `0` to `n - 1` and `n - 1` edges.

You are given a **0-indexed** integer array `nums` of length `n` where `nums[i]` represents the value of the `ith` node. You are also given a 2D integer array `edges` of length `n - 1` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the tree.

Remove two **distinct** edges of the tree to form three connected components. For a pair of removed edges, the following steps are defined:

1. Get the XOR of all the values of the nodes for **each** of the three components respectively.
1. The **difference** between the **largest** XOR value and the **smallest** XOR value is the **score** of the pair.
- For example, say the three components have the node values: `[4,5,7]`, `[1,9]`, and `[3,3,3]`. The three XOR values are `4 ^ 5 ^ 7 = ``<u>**6**</u>`, `1 ^ 9 = ``<u>**8**</u>`, and `3 ^ 3 ^ 3 = ``<u>**3**</u>`. The largest XOR value is `8` and the smallest XOR value is `3`. The score is then `8 - 3 = 5`.
Return *the ****minimum**** score of any possible pair of edge removals on the given tree*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2022/05/03/ex1drawio.png)

```plain text
Input: nums = [1,5,5,4,11], edges = [[0,1],[1,2],[1,3],[3,4]]
Output: 9
Explanation: The diagram above shows a way to make a pair of removals.
- The 1st component has nodes [1,3,4] with values [5,4,11]. Its XOR value is 5 ^ 4 ^ 11 = 10.
- The 2nd component has node [0] with value [1]. Its XOR value is 1 = 1.
- The 3rd component has node [2] with value [5]. Its XOR value is 5 = 5.
The score is the difference between the largest and smallest XOR value which is 10 - 1 = 9.
It can be shown that no other pair of removals will obtain a smaller score than 9.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2022/05/03/ex2drawio.png)

```plain text
Input: nums = [5,5,2,4,4,2], edges = [[0,1],[1,2],[5,2],[4,3],[1,3]]
Output: 0
Explanation: The diagram above shows a way to make a pair of removals.
- The 1st component has nodes [3,4] with values [4,4]. Its XOR value is 4 ^ 4 = 0.
- The 2nd component has nodes [1,0] with values [5,5]. Its XOR value is 5 ^ 5 = 0.
- The 3rd component has nodes [2,5] with values [2,2]. Its XOR value is 2 ^ 2 = 0.
The score is the difference between the largest and smallest XOR value which is 0 - 0 = 0.
We cannot obtain a smaller score than 0.
```

**Constraints:**

- `n == nums.length`
- `3 <= n <= 1000`
- `1 <= nums[i] <= 108`
- `edges.length == n - 1`
- `edges[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- `edges` represents a valid tree.
```java
class Solution {
    private int[] subtreeXor;// x 為根的整個子樹的 XOR
    private Set<Integer>[] descendants;
    private List<Integer>[] graph;

    private void dfs(int node, int parent, int[] nums) {
        subtreeXor[node] = nums[node];
        descendants[node].add(node);

        for (int neighbor : graph[node]) {
            if (neighbor != parent) {
                dfs(neighbor, node, nums);
                subtreeXor[node] ^= subtreeXor[neighbor];
                descendants[node].addAll(descendants[neighbor]);
            }
        }
    }

    public int minimumScore(int[] nums, int[][] edges) {
        int n = nums.length;
        graph = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int[] edge : edges) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }

        subtreeXor = new int[n];
        descendants = new HashSet[n];
        for (int i = 0; i < n; i++) 
            descendants[i] = new HashSet<>();

        dfs(0, -1, nums);
        // 整棵樹的 XOR
        int totalXor = subtreeXor[0];
        int minScore = Integer.MAX_VALUE;
        // root 沒有 parent → 不能選
        for (int i = 1; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int xorI = subtreeXor[i];
                int xorJ = subtreeXor[j];
                int val1, val2, val3;

                if (descendants[i].contains(j)) { // j is in i's subtree
                    val1 = xorJ;
                    val2 = xorI ^ xorJ;
                    val3 = totalXor ^ xorI;
                } else if (descendants[j].contains(i)) { // i is in j's subtree
                    val1 = xorI;
                    val2 = xorJ ^ xorI;
                    val3 = totalXor ^ xorJ;
                } else { // Independent subtrees
                    val1 = xorI;
                    val2 = xorJ;
                    val3 = totalXor ^ xorI ^ xorJ;
                }
                
                int maxVal = Math.max(val1, Math.max(val2, val3));
                int minVal = Math.min(val1, Math.min(val2, val3));
                minScore = Math.min(minScore, maxVal - minVal);
            }
        }

        return minScore;
    }
}
```

