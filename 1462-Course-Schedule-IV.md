`Methods:`DP,Floyd-Warshall </br> `Data Structure:`undefined </br> `Difficulty:`Medium </br> `Similar:`undefined </br> 
 There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `ai` first if you want to take course `bi`.

- For example, the pair `[0, 1]` indicates that you have to take course `0` before you can take course `1`.
Prerequisites can also be **indirect**. If course `a` is a prerequisite of course `b`, and course `b` is a prerequisite of course `c`, then course `a` is a prerequisite of course `c`.

You are also given an array `queries` where `queries[j] = [uj, vj]`. For the `jth` query, you should answer whether course `uj` is a prerequisite of course `vj` or not.

Return *a boolean array *`answer`*, where *`answer[j]`* is the answer to the *`jth`* query.*

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/05/01/courses4-1-graph.jpg)

```plain text
Input: numCourses = 2, prerequisites = [[1,0]], queries = [[0,1],[1,0]]
Output: [false,true]
Explanation: The pair [1, 0] indicates that you have to take course 1 before you can take course 0.
Course 0 is not a prerequisite of course 1, but the opposite is true.

```

**Example 2:**

```plain text
Input: numCourses = 2, prerequisites = [], queries = [[1,0],[0,1]]
Output: [false,false]
Explanation: There are no prerequisites, and each course is independent.

```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/05/01/courses4-3-graph.jpg)

```plain text
Input: numCourses = 3, prerequisites = [[1,2],[1,0],[2,0]], queries = [[1,0],[1,2]]
Output: [true,true]

```

**Constraints:**

- `2 <= numCourses <= 100`
- `0 <= prerequisites.length <= (numCourses * (numCourses - 1) / 2)`
- `prerequisites[i].length == 2`
- `0 <= ai, bi <= numCourses - 1`
- `ai != bi`
- All the pairs `[ai, bi]` are **unique**.
- The prerequisites graph has no cycles.
- `1 <= queries.length <= 104`
- `0 <= ui, vi <= numCourses - 1`
- `ui != vi`
```java
class Solution {
    public List<Boolean> checkIfPrerequisite(int numCourses, int[][] prerequisites, int[][] queries) {
        // 初始化可达矩阵
        boolean[][] reachable = new boolean[numCourses][numCourses];
        
        // 填充直接前置课程
        for (int[] pre : prerequisites) {
            reachable[pre[0]][pre[1]] = true;
        }
        
        // 使用 Floyd-Warshall 算法计算所有可达关系
        for (int k = 0; k < numCourses; k++) {
            for (int i = 0; i < numCourses; i++) {
                for (int j = 0; j < numCourses; j++) {
                    if(!reachable[i][j] && reachable[i][k] && reachable[k][j])
                        reachable[i][j] = true;
                }
            }
        }
        
        // 处理查询
        List<Boolean> res = new ArrayList<>();
        for (int[] query : queries) {
            res.add(rea;
            chable[query[0]][query[1]]);
        }
        
        return res;
    }
}

```

