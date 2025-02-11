# 1579. Remove Max Number of Edges to Keep Graph Fully Traversable

Data structure: Union Find
Difficulty: Hard

Alice and Bob have an undirected graph of `n` nodes and three types of edges:

- Type 1: Can be traversed by Alice only.
- Type 2: Can be traversed by Bob only.
- Type 3: Can be traversed by both Alice and Bob.

Given an array `edges` where `edges[i] = [typei, ui, vi]` represents a bidirectional edge of type `typei` between nodes `ui` and `vi`, find the maximum number of edges you can remove so that after removing the edges, the graph can still be fully traversed by both Alice and Bob. The graph is fully traversed by Alice and Bob if starting from any node, they can reach all other nodes.

Return *the maximum number of edges you can remove, or return* `-1` *if Alice and Bob cannot fully traverse the graph.*

**Example 1:**

![https://assets.leetcode.com/uploads/2020/08/19/ex1.png](https://assets.leetcode.com/uploads/2020/08/19/ex1.png)

```
Input: n = 4, edges = [[3,1,2],[3,2,3],[1,1,3],[1,2,4],[1,1,2],[2,3,4]]
Output: 2
Explanation:If we remove the 2 edges [1,1,2] and [1,1,3]. The graph will still be fully traversable by Alice and Bob. Removing any additional edge will not make it so. So the maximum number of edges we can remove is 2.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/08/19/ex2.png](https://assets.leetcode.com/uploads/2020/08/19/ex2.png)

```
Input: n = 4, edges = [[3,1,2],[3,2,3],[1,1,4],[2,1,4]]
Output: 0
Explanation:Notice that removing any edge will not make the graph fully traversable by Alice and Bob.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2020/08/19/ex3.png](https://assets.leetcode.com/uploads/2020/08/19/ex3.png)

```
Input: n = 4, edges = [[3,2,3],[1,1,2],[2,3,4]]
Output: -1
Explanation:In the current graph, Alice cannot reach node 4 from the other nodes. Likewise, Bob cannot reach 1. Therefore it's impossible to make the graph fully traversable.
```

**Constraints:**

- `1 <= n <= 105`
- `1 <= edges.length <= min(105, 3 * n * (n - 1) / 2)`
- `edges[i].length == 3`
- `1 <= typei <= 3`
- `1 <= ui < vi <= n`
- All tuples `(typei, ui, vi)` are distinct.

```java
class Solution {
    public int maxNumEdgesToRemove(int n, int[][] edges) {
        // n個節點 需n-1個edges
        Arrays.sort(edges, (a, b) -> b[0] - a[0]);// type3排前面

        int edgeAdd = 0;

        UnionFind alice = new UnionFind(n);
        UnionFind bob = new UnionFind(n);

        for (int[] edge : edges) {
            int type = edge[0];
            int a = edge[1];
            int b = edge[2];

            switch (type) {
                case 3:
                    if (alice.unite(a, b) | bob.unite(a, b)) // 前後都要計算 故用 |
                        edgeAdd++;
                    break;
                case 2:
                    if (bob.unite(a, b)) 
                        edgeAdd++;
                    break;
                case 1:
                    if (alice.unite(a, b)) 
                        edgeAdd++;
                    break;
            }
        }
        // 每點都有走到 輸出 else 走不完 -1
        return (alice.united() && bob.united()) ? edges.length - edgeAdd : -1;
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