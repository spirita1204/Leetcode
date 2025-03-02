# 673. Number of Longest Increasing Subsequence  

  Methods: DP </br> Difficulty: Medium++ </br> Similar: 300 </br> </br>Given an integer array `nums`, return *the number of longest increasing subsequences.*

**Notice** that the sequence has to be **strictly** increasing.

**Example 1: **

```plain text
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**

```plain text
Input: nums = [2,2,2,2,2]
Output: 5
Explanation: The length of the longest increasing subsequence is 1, and there are 5 increasing subsequences of length 1, so output 5.
```

**Constraints:**

- `1 <= nums.length <= 2000`
- `106 <= nums[i] <= 106`
- The answer is guaranteed to fit inside a 32-bit integer.
```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        // dp[i] => s[1:i]里以s[i]結尾的最長遞增子序列
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int[] counter = new int[nums.length];
        counter[0] = 1;
        for (int i = 1; i < nums.length; i++) {
            int max = Integer.MIN_VALUE;
            int cnt = 0;
            for (int j = 0; j <= i; j++) {
                if (nums[j] < nums[i]) {// 當 遞增
                    if (dp[j] > max) {
                        max = dp[j];
                        cnt = counter[j];// 紀錄個數
                    } else if (dp[j] == max) {
                        cnt += counter[j];// 從之前組合加總
                    }
                    // 改寫原本max = Math.max(max, dp[j]);
                }
            }
            // 避免都是長度1情況
            counter[i] = cnt == 0 ? 1 : cnt;
            dp[i] = (max == Integer.MIN_VALUE) ? 1 : max + 1; // 當前節點為上一段最長節點+1

        }
        int res = 0;
        int max = 0;
        // 將長度相同且LIS的 其counter相加
        for (int i = 0; i < dp.length; i++) {
            if (dp[i] > max) {
                max = dp[i];
                res = counter[i];
            } else if (dp[i] == max) {
                res += counter[i];
            }
        }
        return res;
    }
}
```

