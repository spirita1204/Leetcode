# 2685. Count the Number of Complete Components  

  Data Structure: Union Find,Graph </br> </br>You are given an integer `n`. There is an **undirected** graph with `n` vertices, numbered from `0` to `n - 1`. You are given a 2D integer array `edges` where `edges[i] = [ai, bi]` denotes that there exists an **undirected** edge connecting vertices `ai` and `bi`.

Return *the number of ****complete connected components**** of the graph*.

A **connected component** is a subgraph of a graph in which there exists a path between any two vertices, and no vertex of the subgraph shares an edge with a vertex outside of the subgraph.

A connected component is said to be **complete** if there exists an edge between every pair of its vertices.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2023/04/11/screenshot-from-2023-04-11-23-31-23.png)

```plain text
Input: n = 6, edges = [[0,1],[0,2],[1,2],[3,4]]
Output: 3
Explanation: From the picture above, one can see that all of the components of this graph are complete.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2023/04/11/screenshot-from-2023-04-11-23-32-00.png)

```plain text
Input: n = 6, edges = [[0,1],[0,2],[1,2],[3,4],[3,5]]
Output: 1
Explanation: The component containing vertices 0, 1, and 2 is complete since there is an edge between every pair of two vertices. On the other hand, the component containing vertices 3, 4, and 5 is not complete since there is no edge between vertices 4 and 5. Thus, the number of complete components in this graph is 1.
```

**Constraints:**

- `1 <= n <= 50`
- `0 <= edges.length <= n * (n - 1) / 2`
- `edges[i].length == 2`
- `0 <= ai, bi <= n - 1`
- `ai != bi`
- There are no repeated edges.
Hint 1

Find the connected components of an undirected graph using depth-first search (DFS) or breadth-first search (BFS).

---

Hint 2

For each connected component, count the number of nodes and edges in the component.

---

Hint 3

A connected component is complete if and only if the number of edges in the component is equal to m*(m-1)/2, where m is the number of nodes in the component.

---

```java
class Solution {
    public int countCompleteComponents(int n, int[][] edges) {
        UnionFind unionFind = new UnionFind(n);
        for(int[] edge : edges) {
            unionFind.unite(edge[0], edge[1]);
        }
        Map<Integer, Set<Integer>> componentVertices = new HashMap<>();
        Map<Integer, Integer> componentEdges = new HashMap<>();
        // vertices
        for (int i = 0; i < n; i++) {
            int root = unionFind.findComponent(i);
            componentVertices.computeIfAbsent(root, k -> new HashSet<>()).add(i);
        }
        // edges
        for (int[] edge : edges) {
            int root = unionFind.findComponent(edge[0]);
            componentEdges.put(root, componentEdges.getOrDefault(root, 0) + 1);// 
        }
        int completeCount = 0;
        // n*(n-1)/2
        for (int root : componentVertices.keySet()) {
            int numVertices = componentVertices.get(root).size();
            int expectedEdges = numVertices * (numVertices - 1) / 2;

            if (expectedEdges == componentEdges.getOrDefault(root, 0)) {
                completeCount++;
            }
        }
        return completeCount;
    }
}

class UnionFind {
    int[] component;
    int distinctComponents;
    int[] compCnt;

    public UnionFind(int n) {
        component = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            component[i] = i;
        } // {0,1,2,3,4}
        distinctComponents = n;// 4
    }

    // unite. For example, if previously we have component {0, 4, 4, 4, 4, 6, 7, 7},
    // then invoke this method with a=1, b=5, then after invoke, {0, 4, 4, 4, 5, 7,
    // 7, 7}
    public boolean unite(int a, int b) {
        if (findComponent(a) != findComponent(b)) {
            component[findComponent(a)] = b;
            distinctComponents--;
            return true;
        }
        return false;// 已經相連
    }

    // find and change component
    // for example, if previously we have component: {0, 2, 3, 4, 4, 6, 7, 7}, then
    // after invoke this method with a=1, the component become {0, 4, 4, 4, 4, 6, 7,
    // 7}
    // 找到 input 節點的 root ，可以藉此確定 input 節點屬於哪一個子集
    public int findComponent(int a) {
        if (component[a] != a) {
            component[a] = findComponent(component[a]);
        }
        return component[a];
    }
}
```

