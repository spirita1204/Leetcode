# 684. Redundant Connection

Data structure: Union Find
Difficulty: Medium

Medium

Topics

Companies

In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two **different** vertices chosen from `1` to `n`, and was not an edge that already existed. The graph is represented as an array `edges` of length `n` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the graph.

Return *an edge that can be removed so that the resulting graph is a tree of* `n` *nodes*. If there are multiple answers, return the answer that occurs last in the input.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/05/02/reduntant1-1-graph.jpg](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-1-graph.jpg)

```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/05/02/reduntant1-2-graph.jpg](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-2-graph.jpg)

```
Input: edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
Output: [1,4]

```

**Constraints:**

- `n == edges.length`
- `3 <= n <= 1000`
- `edges[i].length == 2`
- `1 <= ai < bi <= edges.length`
- `ai != bi`
- There are no repeated edges.
- The given graph is connected.

```java
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int length = edges.length;
        UnionFind u = new UnionFind(length);
        int[] res = new int[2];
        for(int i = 0; i < length; i++) {
            if(!u.unite(edges[i][0], edges[i][1])) {
                // 不可union
                res[0] = edges[i][0];
                res[1] = edges[i][1];
            }
        }
        return res;
    }
    
    private class UnionFind {
        int[] component;
        int distinctComponents;

        public UnionFind(int n) {
            component = new int[n + 1];
            for (int i = 0; i <= n; i++) {
                component[i] = i;
            }// {0,1,2,3,4}
            distinctComponents = n;// 4
        }

        // unite. For example, if previously we have component       {0, 4, 4, 4, 4, 6, 7, 7},
        // then invoke this method with a=1, b=5, then after invoke, {0, 4, 4, 4, 5, 7, 7, 7}
        private boolean unite(int a, int b) {
            if (findComponent(a) != findComponent(b)) {
                component[findComponent(a)] = b;
                distinctComponents--;
                return true;
            }
            return false;// 已經相連
        }

        // find and change component
        // for example, if previously we have component:           {0, 2, 3, 4, 4, 6, 7, 7}, then
        // after invoke this method with a=1, the component become {0, 4, 4, 4, 4, 6, 7, 7}
        // 找到 input 節點的 root ，可以藉此確定 input 節點屬於哪一個子集 
        private int findComponent(int a) {
            if (component[a] != a) {
                component[a] = findComponent(component[a]);
            }
            return component[a];
        }
        // 是否使用n-1條邊
        private boolean united() {
            return distinctComponents == 1;
        }
    }
}
```