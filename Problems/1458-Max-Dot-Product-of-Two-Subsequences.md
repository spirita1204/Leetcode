# 1458. Max Dot Product of Two Subsequences  

  Methods: DP,Recursion </br> Difficulty: Hard </br> </br>Given two arrays `nums1` and `nums2`.

Return the maximum dot product between **non-empty** subsequences of nums1 and nums2 with the same length.

A subsequence of a array is a new array which is formed from the original array by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `[2,3,5]` is a subsequence of `[1,2,3,4,5]` while `[1,5,3]` is not).

**Example 1:**

```plain text
Input: nums1 = [2,1,-2,5], nums2 = [3,0,-6]
Output: 18
Explanation: Take subsequence [2,-2] from nums1 and subsequence [3,-6] from nums2.
Their dot product is (2*3 + (-2)*(-6)) = 18.
```

**Example 2:**

```plain text
Input: nums1 = [3,-2], nums2 = [2,-6,7]
Output: 21
Explanation: Take subsequence [3] from nums1 and subsequence [7] from nums2.
Their dot product is (3*7) = 21.
```

**Example 3:**

```plain text
Input: nums1 = [-1,-1], nums2 = [1,1]
Output: -1
Explanation:Take subsequence [-1] from nums1 and subsequence [1] from nums2.   
Their dot product is -1.   
```

**Constraints:**

- `1 <= nums1.length, nums2.length <= 500`
- `1000 <= nums1[i], nums2[i] <= 1000`
```java
class Solution {
    int[] nums1, nums2;
    int[][] memo;
    int n, m;
    final int NEG_INF = (int) -1e9;

    private int dp(int i, int j) {
        if (i == n || j == m)
            return NEG_INF;
        if (memo[i][j] != Integer.MIN_VALUE)
            return memo[i][j];

        int take = nums1[i] * nums2[j];

        int res = Math.max(
            Math.max(
                // 現在選 (i, j)
                // 後面還可以再選更多 pair
                take + dp(i + 1, j + 1), // take both and continue
                // 只選這一對，直接結束
                take                    // take and end here
            ),
            Math.max(
                // nums1[i] 不用
                // nums2[j] 可能留給後面用
                dp(i + 1, j),           // skip nums1[i] 
                // nums2[j] 不用
                // nums1[i] 留著
                dp(i, j + 1)            // skip nums2[j]
            )
        );
        return memo[i][j] = res;
    }
    // 在 nums1[i..] 與 nums2[j..] 中
    // 選擇「至少一對」元素 所能得到的最大 dot product
    public int maxDotProduct(int[] a, int[] b) {
        nums1 = a;
        nums2 = b;
        n = nums1.length;
        m = nums2.length;

        memo = new int[n][m];
        for (int i = 0; i < n; i++)
            Arrays.fill(memo[i], Integer.MIN_VALUE);

        return dp(0, 0);
    }
}
```

