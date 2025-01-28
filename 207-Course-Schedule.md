# 207. Course Schedule

Data structure: Graph
Difficulty: Medium

**Medium**

13.1K

519

Companies

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take.
To take course 1 you should have finished course 0. So it is possible.

```

**Example 2:**

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take.
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

```

**Constraints:**

- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs prerequisites[i] are **unique**.

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        //prerequisites衝突代表有cycle
        int[][] mat = new int[numCourses][numCourses]; // 每堂課->課 對應關係
        int[] indegree = new int[numCourses];// 每堂課相連關係
        Queue<Integer> q = new LinkedList<>();
         
        for (int i= 0; i< prerequisites.length; i++) {
            int ready = prerequisites[i][0];//當前
            int pre = prerequisites[i][1];//之前 需要
            indegree[ready]++; 
            mat[pre][ready] = 1;

        }
        for(int i = 0; i< numCourses; i++){
            if(indegree[i] == 0) q.offer(i);    
        }

        int seen = 0;// 計算是否都處理完(cycle會處理不完)
        while(!q.isEmpty()){
            int course = q.poll();
            seen++;

            for(int i = 0; i< numCourses; i++) {
                if(mat[course][i] != 0) {//代表有相連關係
                    indegree[i]--;//將原本點刪除 相應i會少1 degree
                    if(indegree[i] == 0) q.offer(i);
                }
            }
        }
        return seen == numCourses;
    }
}
```