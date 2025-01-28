# 274. H-Index

Methods: Binary Search
Difficulty: Medium

Medium

Topics

Companies

Hint

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their `ith` paper, return *the researcher's h-index*.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): The h-index is defined as the maximum value of `h` such that the given researcher has published at least `h` papers that have each been cited at least `h` times.

**Example 1:**

```
Input: citations = [3,0,6,1,5]
Output: 3
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively.
Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.

```

**Example 2:**

```
Input: citations = [1,3,1]
Output: 1

```

**Constraints:**

- `n == citations.length`
- `1 <= n <= 5000`
- `0 <= citations[i] <= 1000`

```java
class Solution {
    public int hIndex(int[] citations) {
        // bs
        int left = 0;
        int right = citations.length;

        while (left < right) {
            int cnt = 0;
            int mid = left + (right - left + 1) / 2;// +1 避免[0]情況
            for (int i = 0; i < citations.length; i++)
                if (citations[i] >= mid)
                    cnt++;
            if(cnt >= mid) left = mid;
            else right = mid - 1;
        }
        return left;
    }
}
```