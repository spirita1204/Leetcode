# 198. House Robber

Methods: DP
Difficulty: Medium

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

```

**Example 2:**

```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.

```

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

```java
class Solution {
    public int rob(int[] nums) {
        1. return recursion(nums, nums.length - 1);

        2. Iterative dp + memory => Acess
        int[] dp = new int[nums.length];
        for(int i = 0; i < nums.length; i++){
            if(i == 0) dp[i] = nums[i];
            else if(i == 1) dp[i] = Math.max(nums[i], dp[i - 1]);
            else dp[i] = Math.max(dp[i - 1], nums[i] + dp[i - 2]);
        }
        return dp[nums.length - 1];

        //3.Iterative dp + 2 variables => Acess(perfect)
        if (nums.length == 0) return 0; 
        int a = 0, b = 0;//只需用兩變數存過程 a代表 現在++(-2)之前     b代表 前個
        for (int num : nums) {
            int tmp = a;
            a = Math.max(b + num, a);
            b = tmp;
        }
        return a;
    }
    1.TLE 用遞迴找
    public int recursion(int[] nums, int i){
        if(i < 0) return 0;
        return Math.max(recursion(nums, i - 2) + nums[i], recursion(nums, i - 1));
    }

}
```