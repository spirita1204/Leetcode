# 3494. Find the Minimum Amount of Time to Brew Potions  

  Methods: Greedy,Prefix Sum </br> Difficulty: Medium </br> </br>You are given two integer arrays, `skill` and `mana`, of length `n` and `m`, respectively.

In a laboratory, `n` wizards must brew `m` potions *in order*. Each potion has a mana capacity `mana[j]` and **must** pass through **all** the wizards sequentially to be brewed properly. The time taken by the `ith` wizard on the `jth` potion is `timeij = skill[i] * mana[j]`.

Since the brewing process is delicate, a potion **must** be passed to the next wizard immediately after the current wizard completes their work. This means the timing must be *synchronized* so that each wizard begins working on a potion **exactly** when it arrives.

Return the **minimum** amount of time required for the potions to be brewed properly.

**Example 1:**

**Input:** skill = [1,5,2,4], mana = [5,1,4,2]

**Output:** 110

**Explanation:**

As an example for why wizard 0 cannot start working on the 1st potion before time `t = 52`, consider the case where the wizards started preparing the 1st potion at time `t = 50`. At time `t = 58`, wizard 2 is done with the 1st potion, but wizard 3 will still be working on the 0th potion till time `t = 60`.

**Example 2:**

**Input:** skill = [1,1,1], mana = [1,1,1]

**Output:** 5

**Explanation:**

1. Preparation of the 0 potion begins at time `t = 0`, and is completed by time `t = 3`.
1. Preparation of the 1 potion begins at time `t = 1`, and is completed by time `t = 4`.
1. Preparation of the 2 potion begins at time `t = 2`, and is completed by time `t = 5`.
**Example 3:   **

**Input:** skill = [1,2,3,4], mana = [1,2]

**Output:** 21

**Constraints:**

- `n == skill.length`
- `m == mana.length`
- `1 <= n, m <= 5000`
- `1 <= mana[i], skill[i] <= 5000`
```java
class Solution {
    public long minTime(int[] skill, int[] mana) {
        int n = skill.length, m = mana.length;
        long[] done = new long[n + 1];
        // 確保每瓶藥水的每位巫師開始時間滿足「對上一瓶」與「上位巫師」的順序約束
        // greedy + prefixSum
        for (int j = 0; j < m; j++) {// 第 j 瓶藥水
            for (int i = 0; i < n; i++) {// 計算每位巫師完成時間
                // done[i] 是前一位巫師完成這瓶藥水的時間
                // done[i + 1] 是這位巫師（編號 i）上一瓶藥水的完成時間
                done[i + 1] = Math.max(done[i + 1], done[i]) + (long) mana[j] * skill[i];
            }
            // 正向時 done[i + 1] 代表「巫師 i 完成第 j 瓶藥水的結束時間」
            // 下一輪（j+1 瓶）時，巫師 i 要知道自己目前的「可用時間」
            for (int i = n - 1; i > 0; i--) {// 把每位巫師的「上一瓶完成時刻」更新成下一輪的基準。
                done[i] = done[i + 1] - (long) mana[j] * skill[i];
            }
        }
        
        return done[n];
    }
}
```

