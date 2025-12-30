# 3362. Zero Array Transformation III  

  Methods: Greedy </br> Data Structure: Heap </br> Difficulty: Medium </br> </br>You are given an integer array `nums` of length `n` and a 2D array `queries` where `queries[i] = [li, ri]`.

Each `queries[i]` represents the following action on `nums`:

- Decrement the value at each index in the range `[li, ri]` in `nums` by **at most **1.
- The amount by which the value is decremented can be chosen **independently** for each index.
A **Zero Array** is an array with all its elements equal to 0.

Return the **maximum **number of elements that can be removed from `queries`, such that `nums` can still be converted to a **zero array** using the *remaining* queries. If it is not possible to convert `nums` to a **zero array**, return -1.

**Example 1:**

**Input:** nums = [2,0,2], queries = [[0,2],[0,2],[1,1]]

**Output:** 1

**Explanation:**

After removing `queries[2]`, `nums` can still be converted to a zero array.

- Using `queries[0]`, decrement `nums[0]` and `nums[2]` by 1 and `nums[1]` by 0.
- Using `queries[1]`, decrement `nums[0]` and `nums[2]` by 1 and `nums[1]` by 0.
**Example 2:**

**Input:** nums = [1,1,1,1], queries = [[1,3],[0,2],[1,3],[1,2]]

**Output:** 2

**Explanation:**

We can remove `queries[2]` and `queries[3]`.

**Example 3:**

**Input:** nums = [1,2,3,4], queries = [[0,3]]

**Output:** -1

**Explanation:**

`nums` cannot be converted to a zero array even after using all the queries.

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`
- `1 <= queries.length <= 105`
- `queries[i].length == 2`
- `0 <= li <= ri < nums.length`
```java
class Solution {
    public int maxRemoval(int[] nums, int[][] queries) {
        // queries.length - 最少必要 queries
        int n = nums.length;
        int q = queries.length;
        List<List<Integer>> starts = new ArrayList<>(n);
        for (int i = 0; i < n; i++)
            starts.add(new ArrayList<>());
        for (int[] qr : queries)
            starts.get(qr[0]).add(qr[1]);

        Queue<Integer> avail = new PriorityQueue<>(Comparator.reverseOrder());// 優先選擇影響範圍更大的查詢。
        Queue<Integer> active = new PriorityQueue<>();// 當前活躍的查詢

        int chosen = 0;   
        // greedy  
        for (int i = 0; i < n; i++) {
            for (int r : starts.get(i))
                avail.offer(r);
            // 移除已經過期的 active query
            while (!active.isEmpty() && active.peek() < i)
                active.poll();
            // 算目前還缺幾次「減 1」
            int need = nums[i] - active.size();
            while (need-- > 0) {
                while (!avail.isEmpty() && avail.peek() < i)
                    avail.poll(); // 已經不可能覆蓋 i

                if (avail.isEmpty())
                    return -1; // 沒 query 可選，直接失敗

                active.offer(avail.poll());
                chosen++;
            }
        }
        return q - chosen;
    }
}
```

