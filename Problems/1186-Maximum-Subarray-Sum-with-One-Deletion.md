# 1186. Maximum Subarray Sum with One Deletion  

  Methods: DP </br> Difficulty: Medium </br> </br>Given an array of integers, return the maximum sum for a **non-empty** subarray (contiguous elements) with at most one element deletion. In other words, you want to choose a subarray and optionally delete one element from it so that there is still at least one element left and the sum of the remaining elements is maximum possible.

Note that the subarray needs to be **non-empty** after deleting one element.

**Example 1: **

```plain text
Input: arr = [1,-2,0,3]
Output: 4
Explanation:Because we can choose [1, -2, 0, 3] and drop -2, thus the subarray [1, 0, 3] becomes the maximum value.
```

**Example 2:**

```plain text
Input: arr = [1,-2,-2,3]
Output: 3
Explanation:We just choose [3] and it's the maximum sum.
```

**Example 3:**

```plain text
Input: arr = [-1,-1,-1,-1]
Output: -1
Explanation: The final subarray needs to be non-empty. You can't choose [-1] and delete -1 from it, then get an empty subarray to make the sum equals to 0.
```

**Constraints:**

- `1 <= arr.length <= 105`
- `104 <= arr[i] <= 104`
```java
class Solution {
    public int maximumSum(int[] arr) {
        // 0: 以當前元素結尾沒有行使刪除
        // 1: 以當前元素結尾有行使刪除
        int len = arr.length;
        int[][] dp = new int[len + 1][2];
        dp[0][0] = -10000;
        dp[0][1] = -10000;
        int res = Integer.MIN_VALUE;

        for(int i = 1; i <= len; i++) {
            // 沒有 = 上次沒有or 當前而已
            dp[i][0] = Math.max(dp[i - 1][0] + arr[i - 1], arr[i - 1]);
            // 有 = 當前刪除or 之前刪除過
            dp[i][1] = Math.max(dp[i - 1][0], dp[i - 1][1] + arr[i - 1]);
            
            res = Math.max(res, Math.max(dp[i][0], dp[i][1]));
        }
        return res;
    }
}
```

