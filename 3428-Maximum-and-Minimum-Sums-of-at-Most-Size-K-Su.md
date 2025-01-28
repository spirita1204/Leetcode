# 3428. Maximum and Minimum Sums of at Most Size K Subsequences

Methods: Combinatorics, DP
Difficulty: Medium++

You are given an integer array `nums` and a positive integer `k`. Return the sum of the **maximum** and **minimum** elements of all**subsequences** of nums with **at most** k elements. Since the answer may be very large, return it **modulo** `109 + 7`.

---

**Example 1:**

**Input:** nums = [1,2,3], k = 2

**Output:** 24

**Explanation:**

The subsequences of `nums` with at most 2 elements are:

| **Subsequence** | **Minimum** | **Maximum** | **Sum** |
| --- | --- | --- | --- |
| `[1]` | 1 | 1 | 2 |
| `[2]` | 2 | 2 | 4 |
| `[3]` | 3 | 3 | 6 |
| `[1, 2]` | 1 | 2 | 3 |
| `[1, 3]` | 1 | 3 | 4 |
| `[2, 3]` | 2 | 3 | 5 |
| **Final Total** |  |  | 24 |

The output would be 24.

---

**Example 2:**

**Input:** nums = [5,0,6], k = 1

**Output:** 22

**Explanation:**

For subsequences with exactly 1 element, the minimum and maximum values are the element itself. Therefore, the total is `5 + 5 + 0 + 0 + 6 + 6 = 22`.

---

**Example 3:**

**Input:** nums = [1,1,1], k = 2

**Output:** 12

**Explanation:**

The subsequences `[1, 1]` and `[1]` each appear 3 times. For all of them, the minimum and maximum are both 1. Thus, the total is 12.

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`
- `1 <= k <= min(70, nums.length)`

```java
public class Solution {
    final int MOD = (int) (1e9 + 7);

    public int minMaxSums(int[] nums, int k) {
        int len = nums.length + 1;;
        int[][] dp = new int[len][k];
        dp[0][0] = 1;

        // 初始化 DP 表 C(n,k)=C(n−1,k)+C(n−1,k−1)
        // dp[n][k] => n個物品中選擇k個 =>
        //             不選第 n 個物品的方法數 (C(n-1, k)) + 
        //               選第 n 個物品的方法數 (C(n-1, k-1))
        for (int i = 1; i < len; i++) {
            dp[i][0] = 1; // c i取0
            for (int j = 1; j < k; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1];
                if (dp[i][j] >= MOD) {
                    dp[i][j] %= MOD;
                }
            }
        }
        Arrays.sort(nums);
        int total = 0;
        // 計算正序 
        // 11 21 22 31 32 33
        // 1  2  1  3  3  1 選第 n 個物品的方法數 (C(n-1, k-1)) 最大
        for (int i = 0; i < nums.length; i++) {// Cn
            for (int c = 0; c < Math.min(i + 1, k); c++) {// 限制// 取k
                total += (long) nums[i] * dp[i][c] % MOD;
                total %= MOD;
            }
        }
        // 計算逆序
        reverse(nums);
        // 選第 n 個物品的方法數 (C(n-1, k-1)) 最小
        for (int i = 0; i < nums.length; i++) {
            for (int c = 0; c < Math.min(i + 1, k); c++) {
                total += (long) nums[i] * dp[i][c] % MOD;
                total %= MOD;
            }
        }
        return total % MOD;
    }

    private void reverse(int[] arr) {
        int left = 0, right = arr.length - 1;
        while (left < right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
}

```