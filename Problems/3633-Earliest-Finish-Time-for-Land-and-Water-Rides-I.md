# 3633. Earliest Finish Time for Land and Water Rides I  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given two categories of theme park attractions: **land rides** and **water rides**.

- **Land rides   **
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

**Example 2:**

**Input:** landStartTime = [5], landDuration = [3], waterStartTime = [1], waterDuration = [10]

**Output:** 14

**Explanation:**

- Plan A (water ride 0 → land ride 0):
- Plan B (land ride 0 → water ride 0):
Plan A provides the earliest finish time of 14.

**Constraints:**

- `1 <= n, m <= 100`
- `landStartTime.length == landDuration.length == n`
- `waterStartTime.length == waterDuration.length == m`
- `1 <= landStartTime[i], landDuration[i], waterStartTime[j], waterDuration[j] <= 1000`
```java
class Solution {
    public int earliestFinishTime(
            int[] landStartTime,
            int[] landDuration,
            int[] waterStartTime,
            int[] waterDuration) {
        int n = landStartTime.length;
        int m = waterStartTime.length;
        int res = Integer.MAX_VALUE;
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                int land = landStartTime[i] + landDuration[i];
                int land_water = Math.max(land, waterStartTime[j]) + waterDuration[j];
                res = Math.min(res, land_water);

                int water = waterStartTime[j] + waterDuration[j];
                int water_land = Math.max(water, landStartTime[i]) + landDuration[i];
                res = Math.min(res, water_land);
            }
        }
        return res;
    }
}
```

