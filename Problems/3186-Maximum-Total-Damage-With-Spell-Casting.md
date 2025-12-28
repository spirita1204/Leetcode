# 3186. Maximum Total Damage With Spell Casting  

  Methods: DP,Sort </br> Data Structure: Hash Table </br> Difficulty: Medium </br> </br>A magician has various spells.

You are given an array `power`, where each element represents the damage of a spell. Multiple spells can have the same damage value.

It is a known fact that if a magician decides to cast a spell with a damage of `power[i]`, they **cannot** cast any spell with a damage of `power[i] - 2`, `power[i] - 1`, `power[i] + 1`, or `power[i] + 2`.

Each spell can be cast **only once**.

Return the **maximum** possible *total damage* that a magician can cast.

**Example 1:**

**Input:** power = [1,1,3,4]

**Output:** 6

**Explanation:**

The maximum possible damage of 6 is produced by casting spells 0, 1, 3 with damage 1, 1, 4.

**Example 2:**

**Input:** power = [7,1,6,6]

**Output:** 13

**Explanation:**

The maximum possible damage of 13 is produced by casting spells 1, 2, 3 with damage 1, 6, 6.

**Constraints:   **

- `1 <= power.length <= 105`
- `1 <= power[i] <= 109`
```java
class Solution {
    public long maximumTotalDamage(int[] power) {
        // 類似House Robber
        TreeMap<Integer, Integer> count = new TreeMap<>();
        for (int p : power) 
            count.put(p, count.getOrDefault(p, 0) + 1);
        
        List<int[]> vec = new ArrayList<>();
        vec.add(new int[] { -1000000000, 0 });
        for (Map.Entry<Integer, Integer> e : count.entrySet()) 
            vec.add(new int[] { e.getKey(), e.getValue() });
        
        int n = vec.size();
        // dp f[i] = 以 vec[i] 當作最後一個選的傷害值時，能得到的最大總傷害
        long[] f = new long[n];
        long mx = 0;
        long ans = 0;
        int j = 1;// 左指標
        for (int i = 1; i < n; i++) {// 右指標
            while (j < i && vec.get(j)[0] < vec.get(i)[0] - 2) {// 只允許選：傷害值 ≤ current - 3
                mx = Math.max(mx, f[j]);
                j++;
            }
            f[i] = mx + 1L * vec.get(i)[0] * vec.get(i)[1];
            ans = Math.max(ans, f[i]);
        }
        return ans;
    }
}
```

