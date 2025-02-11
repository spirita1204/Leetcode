# 213. House Robber II

Methods: DP
Difficulty: Medium

**Medium**

8.2K

118

Companies

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

**Example 1:**

```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

```

**Example 2:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

```

**Example 3:**

```
Input: nums = [1,2,3]
Output: 3

```

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1) return nums[0];
        //判斷從0~n-2和 1~n-1誰比較大
        return Math.max(rob(nums, 0, nums.length- 2), rob(nums, 1, nums.length- 1));
    }

    public int rob(int[] nums, int p1, int p2){
        int[] dp = new int[nums.length];
        for(int i = p1; i <= p2; i++){
            if(i == p1) dp[i] = nums[i];
            else if(i == p1 + 1) dp[i] = Math.max(nums[i], dp[i - 1]);
            else dp[i] = Math.max(dp[i - 1], nums[i] + dp[i - 2]);
        }
        return dp[p2];
    }
}
```