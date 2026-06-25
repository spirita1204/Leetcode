# 3635. Earliest Finish Time for Land and Water Rides II  

  Methods: Greedy </br> Difficulty: Medium </br> </br>You are given two categories of theme park attractions: **land rides** and **water rides**.

- **Land rides**
- **Water rides**
A tourist must experience **exactly one** ride from **each** category, in **either order**.

- A ride may be started at its opening time or **any later moment**.
- If a ride is started at time `t`, it finishes at time `t + duration`.
- Immediately after finishing one ride the tourist may board the other (if it is already open) or wait until it opens.
Return the **earliest possible time** at which the tourist can finish both rides.

**Example 1:**

**Input:** landStartTime = [2,8], landDuration = [4,1], waterStartTime = [6], waterDuration = [3]

**Output:** 9

**Explanation:**

- Plan A (land ride 0 → water ride 0):
- Plan B (water ride 0 → land ride 1):
- Plan C (land ride 1 → water ride 0):
- Plan D (water ride 0 → land ride 0):
Plan A gives the earliest finish time of 9.

**Example 2:  **

**Input:** landStartTime = [5], landDuration = [3], waterStartTime = [1], waterDuration = [10]   

**Output:** 14  

**Explanation:   **

- Plan A (water ride 0 → land ride 0):
- Plan B (land ride 0 → water ride 0):
Plan A provides the earliest finish time of 14.   

**Constraints:  **

- `1 <= n, m <= 5 * 104`
- `landStartTime.length == landDuration.length == n`
- `waterStartTime.length == waterDuration.length == m`
- `1 <= landStartTime[i], landDuration[i], waterStartTime[j], waterDuration[j] <= 105`
```java
class Solution {   
    final static int MAX = 300005;

    public int earliestFinishTime(int[] la, int[] lb, int[] wa, int[] wb) {
        int l = MAX, w = MAX, minL = MAX, minW = MAX;
        int n = la.length, m = wa.length;

        for (int i = 0; i < n; i++)  
            l = Math.min(l, la[i] + lb[i]);
   
        for (int i = 0; i < m; i++) {
            w = Math.min(w, wa[i] + wb[i]);  
            minL = Math.min(minL, Math.max(wa[i], l) + wb[i]);
        }   

        for (int i = 0; i < n; i++)
            minW = Math.min(minW, Math.max(la[i], w) + lb[i]);

        return Math.min(minW, minL);
    }
}
```



