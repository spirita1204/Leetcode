# 413. Arithmetic Slices

Methods: DP
Difficulty: Medium

**Medium**

4.8K

279

Companies

An integer array is called arithmetic if it consists of **at least three elements** and if the difference between any two consecutive elements is the same.

- For example, `[1,3,5,7,9]`, `[7,7,7,7]`, and `[3,-1,-5,-9]` are arithmetic sequences.

Given an integer array `nums`, return *the number of arithmetic **subarrays** of* `nums`.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: 3
Explanation: We have 3 arithmetic slices in nums: [1, 2, 3], [2, 3, 4] and [1,2,3,4] itself.

```

**Example 2:**

```
Input: nums = [1]
Output: 0

```

**Constraints:**

- `1 <= nums.length <= 5000`
- `1000 <= nums[i] <= 1000`

```java
class Solution {
    public int numberOfArithmeticSlices(int[] nums) {
        if(nums.length < 3) return 0;
        int[] dp = new int[nums.length];// 到第i點之前 Arithmetic Slices之組合
        /**
        if(i區間同)
            dp[i] = dp[i - 1] + 1
        ex : 1 2 3 4 5 6    
             0 0 1 2 3 4 
         */
        int interval = nums[1] - nums[0];// 地1,2區間
        int res = 0;

        for(int i= 2; i< nums.length; i++){
            if(nums[i] - nums[i-1] == interval){
                dp[i] = dp[i - 1] + 1;
                res += dp[i];
            }else { 
                interval = nums[i] - nums[i-1];
            }
        }

        return res;
    }
}
```