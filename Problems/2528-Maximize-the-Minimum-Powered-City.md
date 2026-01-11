# 2528. Maximize the Minimum Powered City  

  Methods: Greedy,Binary Search,Sliding Window </br> Difficulty: Hard </br> </br>You are given a **0-indexed** integer array `stations` of length `n`, where `stations[i]` represents the number of power stations in the `ith` city.     

Each power station can provide power to every city in a fixed **range**. In other words, if the range is denoted by `r`, then a power station at city `i` can provide power to all cities `j` such that `|i - j| <= r` and `0 <= i, j <= n - 1`.

- Note that `|x|` denotes **absolute** value. For example, `|7 - 5| = 2` and `|3 - 10| = 7`.
The **power** of a city is the total number of power stations it is being provided power from.

The government has sanctioned building `k` more power stations, each of which can be built in any city, and have the same range as the pre-existing ones.

Given the two integers `r` and `k`, return *the ****maximum possible minimum power**** of a city, if the additional power stations are built optimally.*

**Note** that you can build the `k` power stations in multiple cities.

**Example 1:**

```plain text
Input: stations = [1,2,4,5,0], r = 1, k = 2
Output: 5
Explanation:
One of the optimal ways is to install both the power stations at city 1.
So stations will become [1,4,4,5,0].
- City 0 is provided by 1 + 4 = 5 power stations.
- City 1 is provided by 1 + 4 + 4 = 9 power stations.
- City 2 is provided by 4 + 4 + 5 = 13 power stations.
- City 3 is provided by 5 + 4 = 9 power stations.
- City 4 is provided by 5 + 0 = 5 power stations.
So the minimum power of a city is 5.
Since it is not possible to obtain a larger power, we return 5.
```

**Example 2:**

```plain text
Input: stations = [4,4,4,4], r = 0, k = 3
Output: 4
Explanation:
It can be proved that we cannot make the minimum power of a city greater than 4.
```

**Constraints:**

- `n == stations.length`
- `1 <= n <= 105`
- `0 <= stations[i] <= 105`
- `0 <= r <= n - 1`
- `0 <= k <= 109`
```java
class Solution {
    public long maxPower(int[] stations, int r, long k) {
        int n = stations.length;
        long[] power = new long[n];// 當前城市 i 可被覆蓋到的 station 總數
        long window = 0;
        int windowSize = 2 * r + 1;
        // 計算當前城市 i 可被覆蓋到的 station 總數
        for (int j = 0; j <= Math.min(n - 1, r); j++) 
            window += stations[j];
        for (int i = 0; i < n; i++) {
            power[i] = window;
            int removeIdx = i - r;
            if (removeIdx >= 0) 
                window -= stations[removeIdx];
            int addIdx = i + r + 1;
            if (addIdx < n) 
                window += stations[addIdx];
        }
        //
        long low = 0;
        long high = Arrays.stream(power).max().orElse(0L) + k;
        long best = 0;
        while (low <= high) {
            long mid = low + (high - low) / 2;
            if (canReach(power, r, k, mid)) {
                best = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return best;
    }
    // 我最多用 k 個新電站, 能讓 所有城市電力 ≥ target？
    private boolean canReach(long[] power, int r, long k, long target) {
        int n = power.length;
        long used = 0L;
        long[] diff = new long[n + 1];
        long curAdd = 0L;//目前位置 i 所有「之前新增電站」對這裡造成的累積影響

        for (int i = 0; i < n; i++) {
            curAdd += diff[i];
            long total = power[i] + curAdd;
            if (total < target) {
                long need = target - total;
                used += need;
                if (used > k) return false;
                curAdd += need;
                int end = Math.min(n, i + 2 * r + 1);// 加在「城市 i + r」是最優 可以覆蓋前後 greedy
                diff[end] -= need;
            }
        }
        return true;
    }
}
```

