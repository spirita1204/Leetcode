# 2406. Divide Intervals Into Minimum Number of Groups  

  Methods: Greedy </br> Data Structure: Heap </br> Difficulty: Medium </br> </br>You are given a 2D integer array `intervals` where `intervals[i] = [lefti, righti]` represents the **inclusive** interval `[lefti, righti]`.

You have to divide the intervals into one or more **groups** such that each interval is in **exactly** one group, and no two intervals that are in the same group **intersect** each other.

Return *the ****minimum**** number of groups you need to make*.

Two intervals **intersect** if there is at least one common number between them. For example, the intervals `[1, 5]` and `[5, 8]` intersect.

**Example 1:**

```plain text
Input: intervals = [[5,10],[6,8],[1,5],[2,3],[1,10]]
Output: 3
Explanation: We can divide the intervals into the following groups:
- Group 1: [1, 5], [6, 8].
- Group 2: [2, 3], [5, 10].
- Group 3: [1, 10].
It can be proven that it is not possible to divide the intervals into fewer than 3 groups.

```

**Example 2:**

```plain text
Input: intervals = [[1,3],[5,6],[8,10],[11,13]]
Output: 1
Explanation: None of the intervals overlap, so we can put all of them in one group.

```

**Constraints:**

- `1 <= intervals.length <= 105`
- `intervals[i].length == 2`
- `1 <= lefti <= righti <= 106`
```java
class Solution {
    public int minGroups(int[][] intervals) {
        // [1, 5] [1, 10] [2, 3] [5 10] [6 8]
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? a[1] - b[1]:a[0] - b[0]);
        int num = 0;
        Queue<Integer> pq = new PriorityQueue<>();// 紀錄每組最後index 
        for(int[] e : intervals) {
            if(!pq.isEmpty()) {
                int minLast = pq.peek();
                if(e[0] <= minLast) {
                    num++;
                } else {
                    pq.poll();
                }
                pq.offer(e[1]);
            } else 
                pq.offer(e[1]);
        }
        return num + 1;
    }
}
```

