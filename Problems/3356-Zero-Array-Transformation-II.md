# 3356. Zero Array Transformation II  

  Methods: Prefix Sum,Binary Search </br> Difficulty: Medium++ </br> </br>You are given an integer array `nums` of length `n` and a 2D array `queries` where `queries[i] = [li, ri, vali]`.

Each `queries[i]` represents the following action on `nums`:

- Decrement the value at each index in the range `[li, ri]` in `nums` by **at most** `vali`.
- The amount by which each value is decremented can be chosen **independently** for each index.
A **Zero Array** is an array with all its elements equal to 0.

Return the **minimum** possible **non-negative** value of `k`, such that after processing the first `k` queries in **sequence**, `nums` becomes a **Zero Array**. If no such `k` exists, return -1.

---

**Example 1:**

**Input:** nums = [2,0,2], queries = [[0,2,1],[0,2,1],[1,1,3]]

**Output:** 2

**Explanation:**

- **For i = 0 (l = 0, r = 2, val = 1):**
- **For i = 1 (l = 0, r = 2, val = 1):**
---

**Example 2:**

**Input:** nums = [4,3,2,1], queries = [[1,3,2],[0,2,1]]

**Output:** -1

**Explanation:**

- **For i = 0 (l = 1, r = 3, val = 2):**
- **For i = 1 (l = 0, r = 2, val = 1):**
**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 5 * 105`
- `1 <= queries.length <= 105`
- `queries[i].length == 3`
- `0 <= li <= ri < nums.length`
- `1 <= vali <= 5`
```java
class Solution {
    public int minZeroArray(int[] nums, int[][] queries) {
        int n = nums.length;
        int left = 1;
        int right = queries.length;
        // prefixSum
        if (!canMakeZeroArray(right, nums, queries)) return -1;
        // all zero
        int cnt = 0;
        for(int i: nums)
            if(i == 0)
                cnt++;
        if(cnt == n) return 0;
        // binary search 
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (canMakeZeroArray(mid, nums, queries)) 
                right = mid;
            else 
                left = mid + 1;
        }
        return left;
    }

    private boolean canMakeZeroArray(int k, int[] nums, int[][] queries) {
        int n = nums.length;
        int[] diff = new int[n + 1];
        for (int i = 0; i < k; i++) {
            int left = queries[i][0];
            int right = queries[i][1];

            diff[left] += queries[i][2];
            diff[right + 1] -= queries[i][2];
        }
        int currVal = 0;
        for (int i = 0; i < n; i++) {
            currVal += diff[i];
            if (currVal < nums[i]) return false;
        }
        return true;
    }
}
```

