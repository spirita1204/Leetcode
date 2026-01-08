# 2147. Number of Ways to Divide a Long Corridor  

  Methods: Math </br> Difficulty: Hard </br> </br>Along a long library corridor, there is a line of seats and decorative plants. You are given a **0-indexed** string `corridor` of length `n` consisting of letters `'S'` and `'P'` where each `'S'` represents a seat and each `'P'` represents a plant.

One room divider has **already** been installed to the left of index `0`, and **another** to the right of index `n - 1`. Additional room dividers can be installed. For each position between indices `i - 1` and `i` (`1 <= i <= n - 1`), at most one divider can be installed.  

Divide the corridor into non-overlapping sections, where each section has **exactly two seats** with any number of plants. There may be multiple ways to perform the division. Two ways are **different** if there is a position with a room divider installed in the first way but not in the second way.

Return *the number of ways to divide the corridor*. Since the answer may be very large, return it **modulo** `109 + 7`. If there is no way, return `0`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/12/04/1.png)

```plain text
Input: corridor = "SSPPSPS"
Output: 3
Explanation: There are 3 different ways to divide the corridor.
The black bars in the above image indicate the two room dividers already installed.
Note that in each of the ways, each section has exactly two seats.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/12/04/2.png)

```plain text
Input: corridor = "PPSPSP"
Output: 1
Explanation: There is only 1 way to divide the corridor, by not installing any additional dividers.
Installing any would create some section that does not have exactly two seats.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/12/12/3.png)

```plain text
Input: corridor = "S"
Output: 0
Explanation: There is no way to divide the corridor because there will always be a section that does not have exactly two seats.
```

**Constraints:**

- `n == corridor.length`
- `1 <= n <= 105`
- `corridor[i]` is either `'S'` or `'P'`.
```java
class Solution {
       public int numberOfWays(String s) {
        // 上一個 'S' 的 index
        // 目前遇到的 'S' 總數
        long res = 1, j = 0, k = 0;
        long mod = (long)1e9 + 7;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == 'S') {
                if (++k > 2 && k % 2 == 1)
                    res = res * (i - j) % mod;
                j = i;
            }
        }
        // k = 1 → 第 1 個 S（房間未完成）
        // k = 2 → 第 2 個 S（第一個房間完成）
        // k = 3 → 第二個房間的 第 1 個 S
        // k 為奇數（且 >2）的位置，都是「新房間的第一個 S」
        return k % 2 == 0 && k > 0 ? (int)res : 0;
    }
}
```

