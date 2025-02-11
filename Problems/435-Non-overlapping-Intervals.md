# 435. Non-overlapping Intervals

Methods: Pointer
Difficulty: Medium

[Easy C++ solution with drawing - Non-overlapping Intervals - LeetCode](https://leetcode.com/problems/non-overlapping-intervals/solutions/1157602/easy-c-solution-with-drawing/?envType=study-plan&id=data-structure-ii&orderBy=most_votes)

**Medium**

5.7K

156

Companies

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping*.

**Example 1:**

```
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.

```

**Example 2:**

```
Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of the intervals non-overlapping.

```

**Example 3:**

```
Input: intervals = [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.

```

**Constraints:**

- `1 <= intervals.length <= 105`
- `intervals[i].length == 2`
- `5 * 104 <= starti < endi <= 5 * 104`

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int count = 0;
        int l = 0;
        int r = 1;
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        while(r < intervals.length){
            if(intervals[l][1] <= intervals[r][0]){//兩區間無交集
                l = r;
                r++;
            }else if(intervals[l][1] <= intervals[r][1]){//有相交,既第一個情況 只需探段後段 將右丟到=>可減少後續可能重複
                count++;
                r++;
            }else if(intervals[l][1] > intervals[r][1]){//包含 將大的那部分丟到留小
                count++;
                l = r;
                r++;
            }
        }
        return count;
    }
}
```