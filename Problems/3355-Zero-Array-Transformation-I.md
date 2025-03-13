# 3355. Zero Array Transformation I  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>You are given an integer array `nums` of length `n` and a 2D array `queries`, where `queries[i] = [li, ri]`.

For each `queries[i]`:

- Select a  of indices within the range `[li, ri]` in `nums`.
- Decrement the values at the selected indices by 1.
A **Zero Array** is an array where all elements are equal to 0.

Return `true` if it is *possible* to transform `nums` into a **Zero Array **after processing all the queries sequentially, otherwise return `false`.

**Example 1:**

**Input:** nums = [1,0,1], queries = [[0,2]]

**Output:** true

**Explanation:**

- **For i = 0: **
**Example 2:**

**Input:** nums = [4,3,2,1], queries = [[1,3],[0,2]]

**Output:** false

**Explanation:**

- **For i = 0:**
- **For i = 1:**
**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`
- `1 <= queries.length <= 105`
- `queries[i].length == 2`
- `0 <= li <= ri < nums.length`
```java
class Solution {
    public boolean isZeroArray(int[] nums, int[][] queries) {
        int[] diff = new int[nums.length + 1];
        // Difference Array 
        for(int[] q : queries) {
            diff[q[0]]--;
            diff[q[1] + 1]++;
        }
        // prefixSum 
        int e = diff[0];
        for(int i = 0; i < diff.length - 1; i++) {
            if(e + nums[i] > 0) 
                return false;
            if(i < diff.length - 1) {
                e += diff[i + 1];
            }
        }
        return true;
    }
}
```

