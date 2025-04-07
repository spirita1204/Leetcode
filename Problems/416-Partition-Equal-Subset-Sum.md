# 416. Partition Equal Subset Sum  

  Methods: DP </br> Difficulty: Medium </br> </br>Given an integer array `nums`, return `true` *if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or *`false`* otherwise*.

**Example 1:**

```plain text
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```plain text
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```

**Constraints:**

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`
## DFS  **Time Limit Exceeded**

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int i: nums) sum += i;

        return dfs(nums, 0, sum, 0);
    }

    private boolean dfs(int[] nums, int idx, int sum, int total) {
        if(total * 2 > sum) return false;
        if(total * 2 == sum) return true;

        for(int i = idx; i< nums.length; i++) {
            boolean equal = dfs(nums, i + 1, sum, total + nums[i]);
            if(equal) return true;
        }
        return false;
    }
}
```

## DP  O(N* S)

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int len = nums.length;
        int sum = 0;
        for (int i : nums)
            sum += i;

        boolean[][] dp = new boolean[len + 1][sum + 1];// 使用前i 元素 可以組合 value j
        dp[0][0] = true;// 什麼 都沒有 等於sum = 0;

        for (int i = 1; i <= len; i++) {
            for (int j = 1; j <= sum / 2; j++) {// sum/ 2後面不計算不影響
                // 兩種情況
                // 1. dp[i - 1][s] = true -> dp[i][s] = true; 不使用第i個 組成sum
                // 2. dp[i - 1][s - nums[i]] = true -> dp[i][s] = true; 使用第i 元素組成sum
                dp[i][j] = dp[i - 1][j] || (j >= nums[i - 1] && dp[i - 1][j - nums[i - 1]]);// 確保j - nums[i] 在範圍
            }
        }
        return (sum % 2 == 0) ? dp[len][sum / 2] : false;// 避免不能整除 誤判ex: nums = [1,5,3]
    }
}
```

## DP  1d

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int len = nums.length;
        int sum = 0;
        for (int i : nums)
            sum += i;
        if (sum % 2 != 0) 
            return false;
        
        sum /= 2;
        // 2d縮減為1d
        boolean[] dp = new boolean[sum + 1];// 使用前i 元素 可以組合 value j
        dp[0] = true;// 什麼 都沒有 等於sum = 0;

        for (int i : nums) {
            for (int j = sum; j > 0; j--) {
                if (j >= i) {
                    dp[j] = dp[j] || dp[j - i];
                }
            }
        }
        return dp[sum];
    }
}
```

