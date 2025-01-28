# 152. Maximum Product Subarray

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

Given an integer array `nums`, find a

subarray

that has the largest product, and return

*the product*

.

The test cases are generated so that the answer will fit in a **32-bit** integer.

**Example 1:**

```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.

```

**Example 2:**

```
Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

```

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `10 <= nums[i] <= 10`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

```java
class Solution {
    public int maxProduct(int[] nums) {
        int len = nums.length;
        int[] dp1 = new int[len];// 最大
        int[] dp2 = new int[len];// 最小
        int res = nums[0];
        // Tip: 每個位置以他為結尾 算最大 最小 Product Subarray
        dp1[0] = nums[0];
        dp2[0] = nums[0];

        for(int i = 1; i< len; i++) {
            // 額外跟負數上層最小做乘法 可能產生最大
            dp1[i] = Math.max(Math.max(dp1[i - 1] * nums[i], nums[i]), dp2[i - 1] * nums[i]);
            // 額外跟負數上層最大做乘法 可能產生最小
            dp2[i] = Math.min(Math.min(dp2[i - 1] * nums[i], nums[i]), dp1[i - 1] * nums[i]);
        
            res = Math.max(res, dp1[i]);
        }
        return res;
    }
}
```