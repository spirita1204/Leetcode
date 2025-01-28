# 1124. Longest Well-Performing Interval

Methods: Prefix Sum
Difficulty: Medium

Medium

Topics

Companies

Hint

We are given `hours`, a list of the number of hours worked per day for a given employee.

A day is considered to be a *tiring day* if and only if the number of hours worked is (strictly) greater than `8`.

A *well-performing interval* is an interval of days for which the number of tiring days is strictly larger than the number of non-tiring days.

Return the length of the longest well-performing interval.

**Example 1:**

```
Input: hours = [9,9,6,0,6,6,9]
Output: 3
Explanation:The longest well-performing interval is [9,9,6].

```

**Example 2:**

```
Input: hours = [6,6,6]
Output: 0

```

**Constraints:**

- `1 <= hours.length <= 104`
- `0 <= hours[i] <= 16`

```java
class Solution {
    public int longestWPI(int[] hours) {
        int res = 0;
        int score = 0;
        int n = hours.length;
        Map<Integer, Integer> seen = new HashMap<>();

        for (int i = 0; i < n; i++) {
            score += hours[i] > 8 ? 1 : -1;
            if (score > 0) {// 代表從頭到當前有 符合最優解條件
                res = i + 1;
            } else {// 代表非從頭 須找出是否有index可與當前score達到符合
                seen.putIfAbsent(score, i);
                if (seen.containsKey(score - 1)) // 代表 c[i:j] = c[j] - c[i] = 1
                    res = Math.max(res, i - seen.get(score - 1));
            }
        }
        return res;
    }
}
```