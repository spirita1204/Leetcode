# 2127. Maximum Employees to Be Invited to a Meeting

Methods: BFS
Data structure: Graph
Difficulty: Hard

A company is organizing a meeting and has a list of `n` employees, waiting to be invited. They have arranged for a large **circular** table, capable of seating **any number** of employees.

The employees are numbered from `0` to `n - 1`. Each employee has a **favorite** person and they will attend the meeting **only if** they can sit next to their favorite person at the table. The favorite person of an employee is **not** themself.

Given a **0-indexed** integer array `favorite`, where `favorite[i]` denotes the favorite person of the `ith` employee, return *the **maximum number of employees** that can be invited to the meeting*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/12/14/ex1.png](https://assets.leetcode.com/uploads/2021/12/14/ex1.png)

```
Input: favorite = [2,2,1,2]
Output: 3
Explanation:
The above figure shows how the company can invite employees 0, 1, and 2, and seat them at the round table.
All employees cannot be invited because employee 2 cannot sit beside employees 0, 1, and 3, simultaneously.
Note that the company can also invite employees 1, 2, and 3, and give them their desired seats.
The maximum number of employees that can be invited to the meeting is 3.

```

**Example 2:**

```
Input: favorite = [1,2,0]
Output: 3
Explanation:
Each employee is the favorite person of at least one other employee, and the only way the company can invite them is if they invite every employee.
The seating arrangement will be the same as that in the figure given in example 1:
- Employee 0 will sit between employees 2 and 1.
- Employee 1 will sit between employees 0 and 2.
- Employee 2 will sit between employees 1 and 0.
The maximum number of employees that can be invited to the meeting is 3.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2021/12/14/ex2.png](https://assets.leetcode.com/uploads/2021/12/14/ex2.png)

```
Input: favorite = [3,0,1,4,1]
Output: 4
Explanation:
The above figure shows how the company will invite employees 0, 1, 3, and 4, and seat them at the round table.
Employee 2 cannot be invited because the two spots next to their favorite employee 1 are taken.
So the company leaves them out of the meeting.
The maximum number of employees that can be invited to the meeting is 4.

```

**Constraints:**

- `n == favorite.length`
- `2 <= n <= 105`
- `0 <= favorite[i] <= n - 1`
- `favorite[i] != i`

```java
class Solution {
    // 1. 拓撲排序處理鏈
    // 通過 inDeg 找到鏈的起點，將它們加入隊列。
    // 通過 BFS 遍歷，逐步減少鏈中指向的節點的入度，更新鏈的長度。
    // 2. 環的處理
    // 使用 DFS 或 BFS 尋找未訪問的節點。
    // 如果發現一個環，計算它的長度。
    // 如果環長度為 2，將其與鏈結合計算。
    // 3. 返回結果
    // 比較兩種情況的最大值：
    // 環的最大長度。
    // 互相喜愛對的總和（包括鏈）。
    public int maximumInvitations(int[] favorite) {
        int n = favorite.length;
        int[] inDeg = new int[n];
        int[] chainLen = new int[n];
        boolean[] visited = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        // [0,1,2,3]
        // [2,2,1,2]  -> [0,1,3,0]
        // 計算每個員工被喜愛的次數
        for (int f : favorite) inDeg[f]++;
        
        // 找到鏈的起點（沒有被任何人喜愛的員工）
        for (int i = 0; i < n; i++) {
            if (inDeg[i] == 0) q.add(i);
        }
        
        // 拓撲排序處理鏈
        while (!q.isEmpty()) {
            int u = q.poll();
            visited[u] = true;
            int v = favorite[u];
            chainLen[v] = Math.max(chainLen[v], chainLen[u] + 1);
            if (--inDeg[v] == 0) q.add(v);
        }
        
        int maxCycle = 0, pairChains = 0;
        
        // 處理環和鏈
        for (int i = 0; i < n; i++) {
            if (visited[i]) continue; // 已經處理過
            int cycleLen = 0, current = i;
            
            // 計算環的長度
            while (!visited[current]) {
                visited[current] = true;
                current = favorite[current];
                cycleLen++;
            }
            
            if (cycleLen == 2) {// 有多個長度為 2 的環
                // 互相喜愛對，包含鏈長度
                pairChains += (2 + chainLen[i] + chainLen[favorite[i]]);
            } else {
                // 一般環
                maxCycle = Math.max(maxCycle, cycleLen);
            }
        }
        
        // 返回最大結果
        return Math.max(maxCycle, pairChains);
    }
}

```