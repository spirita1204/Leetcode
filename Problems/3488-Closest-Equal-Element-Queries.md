# 3488. Closest Equal Element Queries  

  Methods: Binary Search </br> Difficulty: Medium </br> </br>You are given a **circular** array `nums` and an array `queries`.

For each query `i`, you have to find the following:

- The **minimum** distance between the element at index `queries[i]` and **any** other index `j` in the **circular** array, where `nums[j] == nums[queries[i]]`. If no such index exists, the answer for that query should be -1.
Return an array `answer` of the **same** size as `queries`, where `answer[i]` represents the result for query `i`.

**Example 1:**

**Input:** nums = [1,3,1,4,1,3,2], queries = [0,3,5]

**Output:** [2,-1,3]

**Explanation:**

- Query 0: The element at `queries[0] = 0` is `nums[0] = 1`. The nearest index with the same value is 2, and the distance between them is 2.
- Query 1: The element at `queries[1] = 3` is `nums[3] = 4`. No other index contains 4, so the result is -1.
- Query 2: The element at `queries[2] = 5` is `nums[5] = 3`. The nearest index with the same value is 1, and the distance between them is 3 (following the circular path: `5 -> 6 -> 0 -> 1`).
**Example 2:**

**Input:** nums = [1,2,3,4], queries = [0,1,2,3]

**Output:** [-1,-1,-1,-1]

**Explanation:**

Each value in `nums` is unique, so no index shares the same value as the queried element. This results in -1 for all queries.

**Constraints:   **

- `1 <= queries.length <= nums.length <= 105`
- `1 <= nums[i] <= 106`
- `0 <= queries[i] < nums.length`
```java
class Solution {   
    public List<Integer> solveQueries(int[] nums, int[] queries) {
        Map<Integer, List<Integer>> hm = new HashMap<>();
        int n = nums.length;    

        for(int i = 0; i < n; i++) {
            hm.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
        }
        List<Integer> res = new ArrayList<>(queries.length);

        for (int q : queries) {
            int val = nums[q];
            List<Integer> list = hm.get(val);

            // 若只出現一次，直接 -1
            if (list.size() == 1) {
                res.add(-1);
                continue;
            }
            // 二分找插入點（第一個 >= q）
            int idx = Collections.binarySearch(list, q);
            // 1 -> 0, 2, 4
            // 3 -> 1, 5
            // 4 -> 3 
            int leftIdx, rightIdx;
            int size = list.size();

            // 左鄰、右鄰（循環）
            leftIdx  = list.get((idx - 1 + size) % size);
            rightIdx = list.get((idx + 1) % size);

            // 環形距離
            int distRight = circularDist(q, rightIdx, n);
            int distLeft = circularDist(q, leftIdx, n);
            int best = Math.min(distRight, distLeft);

            res.add(best);
        }
        return res;
    }

    /** 兩個索引在環形陣列中的最短距離 */
    private int circularDist(int a, int b, int n) {
        int diff = Math.abs(a - b);
        return Math.min(diff, n - diff);
    }
}
```

