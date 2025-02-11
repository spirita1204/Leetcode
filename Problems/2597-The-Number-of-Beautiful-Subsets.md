# 2597. The Number of Beautiful Subsets

Methods: DFS
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given an array `nums` of positive integers and a **positive** integer `k`.

A subset of `nums` is **beautiful** if it does not contain two integers with an absolute difference equal to `k`.

Return *the number of **non-empty beautiful** subsets of the array* `nums`.

A **subset** of `nums` is an array that can be obtained by deleting some (possibly none) elements from `nums`. Two subsets are different if and only if the chosen indices to delete are different.

**Example 1:**

```
Input: nums = [2,4,6], k = 2
Output: 4
Explanation: The beautiful subsets of the array nums are: [2], [4], [6], [2, 6].
It can be proved that there are only 4 beautiful subsets in the array [2,4,6].

```

**Example 2:**

```
Input: nums = [1], k = 1
Output: 1
Explanation: The beautiful subset of the array nums is [1].
It can be proved that there is only 1 beautiful subset in the array [1].

```

**Constraints:**

- `1 <= nums.length <= 20`
- `1 <= nums[i], k <= 1000`

```java
class Solution {
    int res = 0;
    public int beautifulSubsets(int[] nums, int k) {
        int[] cnts = new int[1001];
        dfs(nums, k, 0, cnts);
        return res;
    }
    private void dfs(int[] nums, int k, int idx, int[] cnts) {
        for (int i = idx; i < nums.length; i++) {
            // Check if we can include the current element
            if(nums[i] - k > 0 && cnts[nums[i] - k] > 0) continue;
            if(nums[i] + k <= 1000 && cnts[nums[i] + k] > 0) continue;

            // Include nums[i]
            cnts[nums[i]]++;
            res++; // Increment result for each valid subset

            // Continue to explore next elements
            dfs(nums, k, i + 1, cnts);
            // Backtrack
            cnts[nums[i]]--;
        }
    }
}
```