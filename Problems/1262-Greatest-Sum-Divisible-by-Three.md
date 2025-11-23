# 1262. Greatest Sum Divisible by Three  

  Methods: DP </br> Difficulty: Medium </br> </br>Given an integer array `nums`, return *the ****maximum possible sum ****of elements of the array such that it is divisible by three*.

**Example 1:**

```plain text
Input: nums = [3,6,5,1,8]
Output: 18
Explanation: Pick numbers 3, 6, 1 and 8 their sum is 18 (maximum sum divisible by 3).
```

**Example 2:**

```plain text
Input: nums = [4]
Output: 0
Explanation: Since 4 is not divisible by 3, do not pick any number
```

**Example 3:**

```plain text
Input: nums = [1,2,3,4,4]
Output: 12
Explanation: Pick numbers 1, 3, 4 and 4 their sum is 12 (maximum sum divisible by 3).
```

**Constraints:**

- `1 <= nums.length <= 4 * 104` 
- `1 <= nums[i] <= 104`    
```java
class Solution {
    public int maxSumDivThree(int[] nums) {
        // dp[r] 代表 「目前能湊出總和 % 3 == r 的最大總和」
        int[] dp = new int[3];
        for (int num : nums)
            for (int i : Arrays.copyOf(dp, dp.length))
                dp[(i + num) % 3] = Math.max(dp[(i + num) % 3], i + num);

        return dp[0];
    }
}
```

