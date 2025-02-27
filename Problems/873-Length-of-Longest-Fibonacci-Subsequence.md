# 873. Length of Longest Fibonacci Subsequence  

  Methods: DP </br> Data Structure: Hash Table </br> Difficulty: Medium++ </br> </br>A sequence `x1, x2, ..., xn` is *Fibonacci-like* if:

- `n >= 3`
- `xi + xi+1 == xi+2` for all `i + 2 <= n`
Given a **strictly increasing** array `arr` of positive integers forming a sequence, return *the ****length**** of the longest Fibonacci-like subsequence of* `arr`. If one does not exist, return `0`.

A **subsequence** is derived from another sequence `arr` by deleting any number of elements (including none) from `arr`, without changing the order of the remaining elements. For example, `[3, 5, 8]` is a subsequence of `[3, 4, 5, 6, 7, 8]`.

**Example 1: **

```plain text
Input: arr = [1,2,3,4,5,6,7,8]
Output: 5
Explanation: The longest subsequence that is fibonacci-like: [1,2,3,5,8].
```

**Example 2:**

```plain text
Input: arr = [1,3,7,11,12,14,18]
Output: 3
Explanation:The longest subsequence that is fibonacci-like: [1,11,12], [3,11,14] or [7,11,18].
```

**Constraints:**

- `3 <= arr.length <= 1000`
- `1 <= arr[i] < arr[i + 1] <= 109`
```java
class Solution {
    public int lenLongestFibSubseq(int[] arr) {
        // 定義f[i][j]表示以arr[i]作为最後一個元素，以arr[j]作為倒數第二個元素的最長Fibonacci子序列的長度
        // f[i][j] = max(f[i][j],f[j][k]+1)
        int len = arr.length;
        int[][] dp = new int[len][len];

        Map<Integer, Integer> hm = new HashMap<>();
        // init
        for (int i = 0; i < len; i++) {
            hm.put(arr[i], i);
            for (int j = 0; j < i; j++) {
                dp[i][j] = 2;
            }
        }
        int res = 0;
        // 枚舉所有組合
        for (int i = 2; i < len; i++) {
            for (int j = 1; j < i; j++) {
                int e = arr[i] - arr[j];// Fibonacci 需對應的另點
                if (hm.get(e) != null && hm.get(e) < j) {
                    dp[i][j] = Math.max(dp[i][j], dp[j][hm.get(e)] + 1);
                    res = Math.max(res, dp[i][j]);
                }
            }
        }
        // 組合最後都要加一開始2
        return res;
    }
}
```

