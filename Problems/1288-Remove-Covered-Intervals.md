# 1288. Remove Covered Intervals  

  Data Structure: Heap </br> Difficulty: Medium </br> </br>Given an array `intervals` where `intervals[i] = [li, ri]` represent the interval `[li, ri)`, remove all intervals that are covered by another interval in the list.    

The interval `[a, b)` is covered by the interval `[c, d)` if and only if `c <= a` and `b <= d`.  

Return *the number of remaining intervals*.

**Example 1:**

```plain text
Input: intervals = [[1,4],[3,6],[2,8]]     
Output: 2
Explanation: Interval [3,6] is covered by [2,8], therefore it is removed.
```

**Example 2:**

```plain text
Input: intervals = [[1,4],[2,3]]     
Output: 1
```

**Constraints:**

- `1 <= intervals.length <= 1000`
- `intervals[i].length == 2`
- `0 <= li < ri <= 105`
- All the given intervals are **unique**.    
```java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->{
            if(a[0] == b[0]){
              return  Integer.compare(b[1],a[1]);
            }
            return Integer.compare(a[0],b[0]);
        });
        for(int[] interval : intervals){
            pq.offer(interval);
        }
        int cnt = 1;
        int[] node = pq.poll();
        while(!pq.isEmpty()){
            if(pq.peek()[0] >= node[0] && pq.peek()[1] <= node[1]){
                pq.poll();
            } else{
                cnt++;
                node = pq.poll();
            }
        }
        return cnt;
    }
}
```



