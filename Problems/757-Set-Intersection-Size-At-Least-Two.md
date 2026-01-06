# 757. Set Intersection Size At Least Two  

  Methods: Greedy,Sort </br> Difficulty: Hard </br> </br>You are given a 2D integer array `intervals` where `intervals[i] = [starti, endi]` represents all the integers from `starti` to `endi` inclusively.

A **containing set** is an array `nums` where each interval from `intervals` has **at least two** integers in `nums`.

- For example, if `intervals = [[1,3], [3,7], [8,9]]`, then `[1,2,4,7,8,9]` and `[2,3,4,8,9]` are **containing sets**.
Return *the minimum possible size of a containing set*.

**Example 1:    **

```plain text
Input: intervals = [[1,3],[3,7],[8,9]]
Output: 5
Explanation: let nums = [2, 3, 4, 8, 9].
It can be shown that there cannot be any containing array of size 4.
```

**Example 2:**

```plain text
Input: intervals = [[1,3],[1,4],[2,5],[3,5]]
Output: 3
Explanation: let nums = [2, 3, 4].
It can be shown that there cannot be any containing array of size 2.
```

**Example 3:**

```plain text
Input: intervals = [[1,2],[2,3],[2,4],[4,5]]
Output: 5
Explanation: let nums = [1, 2, 3, 4, 5].
It can be shown that there cannot be any containing array of size 4.
```

**Constraints:**

- `1 <= intervals.length <= 3000`
- `intervals[i].length == 2`
- `0 <= starti < endi <= 108`
```java
class Solution {
    public int intersectionSizeTwo(int[][] intervals) {
        // 右端點最小的區間 因為：
        // 它最早「結束」
        // 超過 end 就完全不能選了
        Arrays.sort(intervals, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return (a[1] != b[1] ? Integer.compare(a[1], b[1]) : Integer.compare(b[0], a[0]));
            }
        });
        // 目前選過的最大那個數
        // 目前選過的第二大數
        int m = 0, largest = -1, second = -1;

        for (int[] interval : intervals) {
            int a = interval[0], b = interval[1];

            boolean isLargestIn = (a <= largest);
            boolean isSecondIn = (a <= second);
            // Case 1：已經有 2 個點在區間內
            if (isLargestIn && isSecondIn)
                continue;// 不用選
            // Case 2：只命中 1 個點 → 補 1 個
            // 情況	                    說明	    要補
            // largest 在、second 不在	已有 1 個	補 1
            // 兩個都不在            	 0 個	    補 2
            m += (isLargestIn ? 1 : 2);
            // 越右邊 → 能覆蓋越多未來區間
            second = (isLargestIn ? largest : b - 1);
            largest = b;
        }

        return m;
    }
}
```

