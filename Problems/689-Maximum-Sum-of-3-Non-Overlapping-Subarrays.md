# 689. Maximum Sum of 3 Non-Overlapping Subarrays

Methods: Pointer, Prefix Sum
Difficulty: Hard

Hard

Topics

Companies

Given an integer array `nums` and an integer `k`, find three non-overlapping subarrays of length `k` with maximum sum and return them.

Return the result as a list of indices representing the starting position of each interval (**0-indexed**). If there are multiple answers, return the lexicographically smallest one.

**Example 1:**

```
Input: nums = [1,2,1,2,6,7,5,1], k = 2
Output: [0,3,5]
Explanation: Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
We could have also taken [2, 1], but an answer of [1, 3, 5] would be lexicographically larger.

```

**Example 2:**

```
Input: nums = [1,2,1,2,1,2,1,2,1], k = 2
Output: [0,2,4]

```

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `1 <= nums[i] < 216`
- `1 <= k <= floor(nums.length / 3)`

```java
class Solution {
    public int[] maxSumOfThreeSubarrays(int[] nums, int k) {
        int n = nums.length;
        int maxSum = 0;
        // Prefix sum 
        int[] prefixSum = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
        }
        int[] leftMaxIndex = new int[n];
        int[] rightMaxIndex = new int[n];
        int[] result = new int[3];
        // Calculate the best starting index for the left subarray for each position
        int currentMaxSum = prefixSum[k] - prefixSum[0];
        for (int i = k; i < n; i++) {
            if (prefixSum[i + 1] - prefixSum[i + 1 - k] > currentMaxSum) {
                leftMaxIndex[i] = i + 1 - k;// 起始點
                currentMaxSum = prefixSum[i + 1] - prefixSum[i + 1 - k];
            } else {
                leftMaxIndex[i] = leftMaxIndex[i - 1];
            }
        }
        // Calculate the best starting index for the right subarray for each position
        rightMaxIndex[n - k] = n - k;
        currentMaxSum = prefixSum[n] - prefixSum[n - k];
        for (int i = n - k - 1; i >= 0; i--) {
            if (prefixSum[i + k] - prefixSum[i] >= currentMaxSum) {
                rightMaxIndex[i] = i;
                currentMaxSum = prefixSum[i + k] - prefixSum[i];
            } else {
                rightMaxIndex[i] = rightMaxIndex[i + 1];
            }
        }
        // Iterate over the middle subarray and calculate the total sum for all valid combinations
        for (int i = k; i <= n - 2 * k; i++) {
            int leftIndex = leftMaxIndex[i - 1];
            int rightIndex = rightMaxIndex[i + k];
            int totalSum =
                (prefixSum[i + k] - prefixSum[i]) + // 中間
                (prefixSum[leftIndex + k] - prefixSum[leftIndex]) + // 左邊
                (prefixSum[rightIndex + k] - prefixSum[rightIndex]);// 右邊

            if (totalSum > maxSum) {
                maxSum = totalSum;
                result[0] = leftIndex;
                result[1] = i;
                result[2] = rightIndex;
            }
        }
        return result;
    }
}
```