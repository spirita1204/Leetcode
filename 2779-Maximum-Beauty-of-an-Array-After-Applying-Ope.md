# 2779. Maximum Beauty of an Array After Applying Operation

Methods: Sliding Window
Difficulty: Medium

You are given a **0-indexed** array `nums` and a **non-negative** integer `k`.

In one operation, you can do the following:

- Choose an index `i` that **hasn't been chosen before** from the range `[0, nums.length - 1]`.
- Replace `nums[i]` with any integer from the range `[nums[i] - k, nums[i] + k]`.

The **beauty** of the array is the length of the longest subsequence consisting of equal elements.

Return *the **maximum** possible beauty of the array* `nums` *after applying the operation any number of times.*

**Note** that you can apply the operation to each index **only once**.

A **subsequence** of an array is a new array generated from the original array by deleting some elements (possibly none) without changing the order of the remaining elements.

```java
class Solution {
    public int maximumBeauty(int[] nums, int k) {
        Arrays.sort(nums);
        // 1 2 4 6
        // 3 5 6 8  +k
        //-1 0 2 4  -k
        // find maximum subarray A[i … j] such that A[j] - A[i] ≤ 2 * k.
        int max = 0;
        int p2 = 1;
        for(int p1 = 0; p1 < nums.length; p1++) {
            while(p2 < nums.length && nums[p2] - nums[p1] <= 2* k) 
                p2++;
            max = Math.max(max, p2 - p1);           
        }
        return max;
    }
}
```