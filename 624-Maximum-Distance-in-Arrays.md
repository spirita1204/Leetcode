# 624. Maximum Distance in Arrays

Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

You are given `m` `arrays`, where each array is sorted in **ascending order**.

You can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers `a` and `b` to be their absolute difference `|a - b|`.

Return *the maximum distance*.

**Example 1:**

```
Input: arrays = [[1,2,3],[4,5],[1,2,3]]
Output: 4
Explanation: One way to reach the maximum distance 4 is to pick 1 in the first or third array and pick 5 in the second array.

```

**Example 2:**

```
Input: arrays = [[1],[1]]
Output: 0

```

**Constraints:**

- `m == arrays.length`
- `2 <= m <= 105`
- `1 <= arrays[i].length <= 500`
- `104 <= arrays[i][j] <= 104`
- `arrays[i]` is sorted in **ascending order**.
- There will be at most `105` integers in all the arrays.

```java
class Solution {
    public int maxDistance(List<List<Integer>> arrays) {
        int len = arrays.size();
        Queue<int[]> pqMax = new PriorityQueue<>((a, b) -> (b[0] - a[0]));
        Queue<int[]> pqMin = new PriorityQueue<>((a, b) -> (a[0] - b[0]));
        for (int i = 0; i < len; i++) {
            int len1 = arrays.get(i).size();
            int eMin = arrays.get(i).get(0);
            int eMax = arrays.get(i).get(len1 - 1);
            pqMax.offer(new int[]{eMax, i});
            pqMin.offer(new int[]{eMin, i});
        }
        int[] max = pqMax.poll();
        int[] min = pqMin.poll();
        if(max[1] != min[1]) return max[0] - min[0];
        else {
            int[] max1 = pqMax.poll();
            int[] min1 = pqMin.poll();
            int res = 0;
            int fir = max1[0] - min[0];
            int sec = max[0] - min1[0];
            res = (fir > sec)? fir: sec;
            return res;
        }
    }
}
```