# 3443. Maximum Manhattan Distance After K Changes  

  Methods: Math </br> Difficulty: Medium </br> </br>You are given a string `s` consisting of the characters `'N'`, `'S'`, `'E'`, and `'W'`, where `s[i]` indicates movements in an infinite grid:

- `'N'` : Move north by 1 unit.
- `'S'` : Move south by 1 unit.
- `'E'` : Move east by 1 unit.
- `'W'` : Move west by 1 unit.
Initially, you are at the origin `(0, 0)`. You can change **at most** `k` characters to any of the four directions.

Find the **maximum** **Manhattan distance** from the origin that can be achieved **at any time** while performing the movements **in order**.

The **Manhattan Distance **between two cells (xi, yi) and (xj, yj) is |xi - xj| + |yi - yj|.

---

**Example 1:**

**Input:** s = "NWSE", k = 1

**Output:** 3

**Explanation:**

Change `s[2]` from `'S'` to `'N'`. The string `s` becomes `"NWNE"`.

The maximum Manhattan distance from the origin that can be achieved is 3. Hence, 3 is the output.

---

**Example 2:**

**Input:** s = "NSWWEW", k = 3

**Output:** 6

**Explanation:**

Change `s[1]` from `'S'` to `'N'`, and `s[4]` from `'E'` to `'W'`. The string `s` becomes `"NNWWWW"`.

The maximum Manhattan distance from the origin that can be achieved is 6. Hence, 6 is the output.

---

**Constraints:**

- `1 <= s.length <= 105`
- `0 <= k <= s.length`
- `s` consists of only `'N'`, `'S'`, `'E'`, and `'W'`.
```java
class Solution {
    public int maxDistance(String s, int k) {
        int res = 0;
        int north = 0, south = 0, east = 0, west = 0;
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == 'N') north++;
            else if (c == 'S') south++;
            else if (c == 'E') east++;
            else if (c == 'W') west++;
            
            int x = Math.abs(north - south);
            int y = Math.abs(east - west);
            int MD = x + y;      // Manhattan Distance
            // 1.抵銷->幫忙
            // 2.到目前為止，有多少步是沒有貢獻到曼哈頓距離的
            int dis = MD + Math.min(2 * k, i + 1 - MD); 

            res = Math.max(res, dis);
        }
        
        return res;
    }
}
```

