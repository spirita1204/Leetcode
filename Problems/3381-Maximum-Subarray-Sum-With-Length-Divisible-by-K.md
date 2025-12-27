# 3381. Maximum Subarray Sum With Length Divisible by K  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>You are given an array of integers `nums` and an integer `k`. 

Return the **maximum** sum of a subarray of `nums`, such that the size of the subarray is **divisible** by `k`.

---

**Example 1:**

**Input:** nums = [1,2], k = 1

**Output:** 3

**Explanation:**

The subarray `[1, 2]` with sum 3 has length equal to 2 which is divisible by 1.

---

**Example 2:**

**Input:** nums = [-1,-2,-3,-4,-5], k = 4

**Output:** -10   

**Explanation:  **

The maximum sum subarray is `[-1, -2, -3, -4]` which has length equal to 4 which is divisible by 4.

---

**Example 3:**

**Input:** nums = [-5,1,2,-3,4], k = 2

**Output:** 4

**Explanation:**

The maximum sum subarray is `[1, 2, -3, 4]` which has length equal to 4 which is divisible by 2

---

**Constraints:**

- `1 <= k <= nums.length <= 2 * 105`      
- `109 <= nums[i] <= 109`          
```java
class Solution {
    public long maxSubarraySum(int[] nums, int k) {
        int n = nums.length;
        // 找一段 連續子陣列，
        // 長度可以被 k 整除，
        // 讓「元素總和最大」。
        long[] prefixSum = new long[n + 1];
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }

        long[] minPrefixSum = new long[k];
        for (int i = 0; i < k; i++) {
            minPrefixSum[i] = Long.MAX_VALUE;
        }

        long maxSum = Long.MIN_VALUE;

        for (int i = 0; i <= n; i++) {
            // 取得目前 index 對 k 的餘數
            int remainder = i % k;

            if (i >= k) {
                maxSum = Math.max(
                    maxSum,
                    prefixSum[i] - minPrefixSum[remainder]
                );
            }
            minPrefixSum[remainder] = Math.min(
                minPrefixSum[remainder],
                prefixSum[i]
            );
        }
        return maxSum == Long.MIN_VALUE ? 0 : maxSum;
    }
}

```

