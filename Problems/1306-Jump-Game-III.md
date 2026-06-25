# 1306. Jump Game III  

  Methods: BFS </br> Difficulty: Medium </br> </br>Given an array of non-negative integers `arr`, you are initially positioned at `start` index of the array. When you are at index `i`, you can jump to `i + arr[i]` or `i - arr[i]`, check if you can reach **any** index with value 0.  

Notice that you can not jump outside of the array at any time.  

**Example 1:    **

```plain text
Input: arr = [4,2,3,0,3,1,2], start = 5
Output: true  
Explanation:  
All possible ways to reach at index 3 with value 0 are:
index 5 -> index 4 -> index 1 -> index 3
index 5 -> index 6 -> index 4 -> index 1 -> index 3
```

**Example 2:**

```plain text
Input: arr = [4,2,3,0,3,1,2], start = 0
Output: true 
Explanation:One possible way to reach at index 3 with value 0 is:
index 0 -> index 4 -> index 1 -> index 3
```

**Example 3:**

```plain text
Input: arr = [3,0,2,1,2], start = 2  
Output: false  
Explanation:There is no way to reach at index 1 with value 0.
```

**Constraints:  **

- `1 <= arr.length <= 5 * 104`
- `0 <= arr[i] < arr.length`
- `0 <= start < arr.length`
```java
class Solution {
    public boolean canReach(int[] arr, int start) {
        int n = arr.length;

        boolean[] visited = new boolean[n];
        Queue<Integer> q = new ArrayDeque<>();

        q.offer(start);

        while (!q.isEmpty()) {  
            int i = q.poll();

            if (i < 0 || i >= n || visited[i])
                continue;

            if (arr[i] == 0)
                return true;

            visited[i] = true;

            q.offer(i + arr[i]);
            q.offer(i - arr[i]);
        }

        return false;
    }
}
```



