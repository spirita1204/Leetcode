# 539. Minimum Time Difference

Methods: Basic logic
Difficulty: Medium

Given a list of 24-hour clock time points in

**"HH:MM"**

format, return

*the minimum **minutes** difference between any two time-points in the list*

.

**Example 1:**

```
Input: timePoints = ["23:59","00:00"]
Output: 1

```

**Example 2:**

```
Input: timePoints = ["00:00","23:59","00:00"]
Output: 0

```

**Constraints:**

- `2 <= timePoints.length <= 2 * 104`
- `timePoints[i]` is in the format **"HH:MM"**.

```java
class Solution {
    public int findMinDifference(List<String> timePoints) {
        Collections.sort(timePoints);
        // 首尾比較
        String fir = timePoints.get(0);
        int fir1 = Integer.parseInt(fir.substring(0, 2)) + 24;
        String fir1Str = String.valueOf(fir1) + fir.substring(2);
        timePoints.add(fir1Str);
        int len = timePoints.size();
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        for(int i = 1; i < len; i++) {
            String s1 = timePoints.get(i - 1);
            String s2 = timePoints.get(i);
            int hour1 = Integer.parseInt(s1.substring(0, 2));
            int hour2 = Integer.parseInt(s2.substring(0, 2));
            int min1 = Integer.parseInt(s1.substring(3, 5));
            int min2 = Integer.parseInt(s2.substring(3, 5));
            int diff = (hour2 - hour1) * 60;
            diff += (min2 - min1);// 兩者差值
            min = Math.min(min, diff);
            max = Math.max(max, diff);
        }
        return Math.min(min, 1440 - max);    
    }
}
```