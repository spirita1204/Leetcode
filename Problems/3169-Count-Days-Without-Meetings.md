# 3169. Count Days Without Meetings  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given a positive integer `days` representing the total number of days an employee is available for work (starting from day 1). You are also given a 2D array `meetings` of size `n` where, `meetings[i] = [start_i, end_i]` represents the starting and ending days of meeting `i` (inclusive).

Return the count of days when the employee is available for work but no meetings are scheduled.

**Note: **The meetings may overlap.

---

**Example 1:**

**Input:** days = 10, meetings = [[5,7],[1,3],[9,10]]

**Output:** 2

**Explanation:**

There is no meeting scheduled on the 4th and 8th days.

---

**Example 2:**

**Input:** days = 5, meetings = [[2,4],[1,3]]

**Output:** 1

**Explanation:**

There is no meeting scheduled on the 5th day.

**Example 3:**

---

**Input:** days = 6, meetings = [[1,6]]

**Output:** 0

**Explanation:**

Meetings are scheduled for all working days.

**Constraints:**

- `1 <= days <= 109`
- `1 <= meetings.length <= 105`
- `meetings[i].length == 2`
- `1 <= meetings[i][0] <= meetings[i][1] <= days`
```java
class Solution {
    public int countDays(int days, int[][] meetings) {
        // 1~3 5~7 9~10
        Arrays.sort(meetings, (a, b) -> a[0] - b[0]);
        int p1 = meetings[0][0], p2 = meetings[0][1];
        int meetingsDays = 0;
        
        for (int i = 0; i < meetings.length; i++) {
            int start = meetings[i][0];
            int end = meetings[i][1];
            if (p2 >= start) {// 有交集
                p2 = Math.max(p2, end);// 當前end大還是之前的 
            } else {// 無交集
                meetingsDays += (p2 - p1 + 1);
                p1 = start;
                p2 = end;
            }
        }
        // 最後一round
        meetingsDays += (p2 - p1 + 1);
    
        return days - meetingsDays;
    }
}
```

