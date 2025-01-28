# 2054. Two Best Non-Overlapping Events

Methods: Binary Search, Prefix Sum
Difficulty: Medium++

You are given a **0-indexed** 2D integer array of `events` where `events[i] = [startTimei, endTimei, valuei]`. The `ith` event starts at `startTimei` and ends at `endTimei`, and if you attend this event, you will receive a value of `valuei`. You can choose **at most** **two** **non-overlapping** events to attend such that the sum of their values is **maximized**.

Return *this **maximum** sum.*

Note that the start time and end time is **inclusive**: that is, you cannot attend two events where one of them starts and the other ends at the same time. More specifically, if you attend an event with end time `t`, the next event must start at or after `t + 1`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/09/21/picture5.png](https://assets.leetcode.com/uploads/2021/09/21/picture5.png)

```
Input: events = [[1,3,2],[4,5,2],[2,4,3]]
Output: 4
Explanation:Choose the green events, 0 and 1 for a sum of 2 + 2 = 4.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/09/21/picture1.png](https://assets.leetcode.com/uploads/2021/09/21/picture1.png)

```
Input: events = [[1,3,2],[4,5,2],[1,5,5]]
Output: 5
Explanation:Choose event 2 for a sum of 5.

```

**Example 3:**

![https://assets.leetcode.com/uploads/2021/09/21/picture3.png](https://assets.leetcode.com/uploads/2021/09/21/picture3.png)

```
Input: events = [[1,5,3],[1,5,1],[6,6,5]]
Output: 8
Explanation:Choose events 0 and 2 for a sum of 3 + 5 = 8.
```

**Constraints:**

- `2 <= events.length <= 105`
- `events[i].length == 3`
- `1 <= startTimei <= endTimei <= 109`
- `1 <= valuei <= 106`

---

Hint 1

How can sorting the events on the basis of their start times help? How about end times?

---

Hint 2

How can we quickly get the maximum score of an interval not intersecting with the interval we chose?

---

```java
class Solution {
    public int maxTwoEvents(int[][] events) {
        // Sort events by endTime
        Arrays.sort(events, (a, b) -> a[1] - b[1]);

        // Prefix max to store the maximum value up to a certain index
        int[] prefixMax = new int[events.length];
        prefixMax[0] = events[0][2];
        for (int i = 1; i < events.length; i++) {
            prefixMax[i] = Math.max(prefixMax[i - 1], events[i][2]);
        }

        int maxSum = 0;

        for (int i = 0; i < events.length; i++) {
            int currentEventValue = events[i][2];

            // Binary search for the latest event that ends before the current event starts
            int left = 0, right = i - 1, lastNonOverlapping = -1;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (events[mid][1] < events[i][0]) {
                    lastNonOverlapping = mid;
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
            // Calculate the sum of the current event and the best non-overlapping event
            int sum = currentEventValue;
            if (lastNonOverlapping != -1) {
                sum += prefixMax[lastNonOverlapping];
            }
            // Update the maximum sum
            maxSum = Math.max(maxSum, sum);
        }

        return maxSum;
    }
}
```