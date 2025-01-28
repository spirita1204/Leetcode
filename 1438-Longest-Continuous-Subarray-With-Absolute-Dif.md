# 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit

Methods: Sliding Window
Data structure: TreeSet
Difficulty: Medium

Medium

Topics

Companies

Hint

Given an array of integers `nums` and an integer `limit`, return the size of the longest **non-empty** subarray such that the absolute difference between any two elements of this subarray is less than or equal to `limit`*.*

**Example 1:**

```
Input: nums = [8,2,4,7], limit = 4
Output: 2
Explanation: All subarrays are:
[8] with maximum absolute diff |8-8| = 0 <= 4.
[8,2] with maximum absolute diff |8-2| = 6 > 4.
[8,2,4] with maximum absolute diff |8-2| = 6 > 4.
[8,2,4,7] with maximum absolute diff |8-2| = 6 > 4.
[2] with maximum absolute diff |2-2| = 0 <= 4.
[2,4] with maximum absolute diff |2-4| = 2 <= 4.
[2,4,7] with maximum absolute diff |2-7| = 5 > 4.
[4] with maximum absolute diff |4-4| = 0 <= 4.
[4,7] with maximum absolute diff |4-7| = 3 <= 4.
[7] with maximum absolute diff |7-7| = 0 <= 4.
Therefore, the size of the longest subarray is 2.

```

**Example 2:**

```
Input: nums = [10,1,2,4,7,2], limit = 5
Output: 4
Explanation: The subarray [2,4,7,2] is the longest since the maximum absolute diff is |2-7| = 5 <= 5.

```

**Example 3:**

```
Input: nums = [4,2,2,2,4,4,2,2], limit = 0
Output: 3

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
- `0 <= limit <= 109`

```java
class Solution {
    public int longestSubarray(int[] nums, int limit) {
        // Tip1 Treeset
        int left = 0;
        // index 
        TreeSet<Integer> set = new TreeSet<>((a, b) -> nums[a] == nums[b] ? a - b : nums[a] - nums[b]);
        set.add(0);
        int res = 1;
        for (int right = 1; right < nums.length; right++) {
            set.add(right);
            // treeset有序 所以相減即為當前limit範圍
            while (nums[set.last()] - nums[set.first()] > limit) {
                set.remove(left);
                left++;
            }
            res = Math.max(res, right - left + 1);
        }
        return res;
    }
}
```