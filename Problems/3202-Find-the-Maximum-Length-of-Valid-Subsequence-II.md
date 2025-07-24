# 3202. Find the Maximum Length of Valid Subsequence II  

  Methods: DP </br> Difficulty: Medium </br> </br>You are given an integer array

```plain text
nums
```

and a

**positive**

integer

```plain text
k
```

.

A subsequence `sub` of `nums` with length `x` is called **valid** if it satisfies:

- `(sub[0] + sub[1]) % k == (sub[1] + sub[2]) % k == ... == (sub[x - 2] + sub[x - 1]) % k.`
Return the length of the

**longest**

**valid**

subsequence of nums

```plain text

```

.

**Example 1:**

**Input:** nums = [1,2,3,4,5], k = 2

**Output:** 5

**Explanation:**

The longest valid subsequence is `[1, 2, 3, 4, 5]`.

**Example 2:**

**Input:** nums = [1,4,2,3,1,4], k = 3

**Output:** 4

**Explanation:**

The longest valid subsequence is `[1, 4, 1, 4]`.

**Constraints:**

- `2 <= nums.length <= 103`
- `1 <= nums[i] <= 107`
- `1 <= k <= 103`
```java
class Solution {
    public int maximumLength(int[] nums, int k) {
        int dp[][] = new int[k][k];
        int max = 0;
        // dp[i][j] where i represents the remainder when nums[j] is divided by k, 
        //            and j represents the length of the subsequence ending at j.
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < k; j++) {
                dp[nums[i] % k][j] = dp[j][nums[i] % k] + 1;
                max = Math.max(max, dp[nums[i] % k][j]);
            }
        }
        return max;
    }
}
```

