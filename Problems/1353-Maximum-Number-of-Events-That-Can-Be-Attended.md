# 1353. Maximum Number of Events That Can Be Attended  

  Methods: Greedy </br> Data Structure: Heap </br> Difficulty: Medium </br> </br>You are given an array of `events` where `events[i] = [startDayi, endDayi]`. Every event `i` starts at `startDayi` and ends at `endDayi`.   

You can attend an event `i` at any day `d` where `startTimei <= d <= endTimei`. You can only attend one event at any time `d`.

Return *the maximum number of events you can attend*.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2020/02/05/e1.png)

```plain text
Input: events = [[1,2],[2,3],[3,4]]
Output: 3
Explanation: You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.
```

**Example 2:**

```plain text
Input: events= [[1,2],[2,3],[3,4],[1,2]]
Output: 4
```

**Constraints:**

- `1 <= events.length <= 105`
- `events[i].length == 2`
- `1 <= startDayi <= endDayi <= 105`
```java
class Solution {
    public int maxEvents(int[][] events) {
        Arrays.sort(events, (a, b) -> a[0] - b[0]);
        
        int day = 0, index = 0 , n = events.length;
        int res = 0;      
        
        Queue<Integer> pq = new PriorityQueue<>();

        while (!pq.isEmpty() || index < n) {
            if (pq.isEmpty()) 
                day = events[index][0];// 起點
            
            while (index < n && events[index][0] <= day) {
                pq.offer(events[index][1]);// 終點
                index++;
            }
            pq.poll();// 取最早結束的
            res++; 
            day++;// 今天用過->隔天   

            while (!pq.isEmpty() && pq.peek() < day) // 清掉比day早的(不會再用)
                pq.poll();
        }
        return res;
    }
}
```

