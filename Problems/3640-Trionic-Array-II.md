# 3640. Trionic Array II  

  Methods: DP </br> Difficulty: Hard </br> </br>You are given an integer array `nums` of length `n`.

A **trionic subarray** is a contiguous subarray `nums[l...r]` (with `0 <= l < r < n`) for which there exist indices `l < p < q < r` such that:

- `nums[l...p]` is **strictly** increasing,
- `nums[p...q]` is **strictly** decreasing,
- `nums[q...r]` is **strictly** increasing.
Return the **maximum** sum of any trionic subarray in `nums`.

**Example 1:**

**Input:** nums = [0,-2,-1,-3,0,2,-1]

**Output:** -4

**Explanation:**

Pick `l = 1`, `p = 2`, `q = 3`, `r = 5`:

- `nums[l...p] = nums[1...2] = [-2, -1]` is strictly increasing (`2 < -1`).
- `nums[p...q] = nums[2...3] = [-1, -3]` is strictly decreasing (`1 > -3`)
- `nums[q...r] = nums[3...5] = [-3, 0, 2]` is strictly increasing (`3 < 0 < 2`).
- Sum = `(-2) + (-1) + (-3) + 0 + 2 = -4`.
**Example 2:**

**Input:** nums = [1,4,2,7]

**Output:** 14

**Explanation:**

Pick `l = 0`, `p = 1`, `q = 2`, `r = 3`:

- `nums[l...p] = nums[0...1] = [1, 4]` is strictly increasing (`1 < 4`).
- `nums[p...q] = nums[1...2] = [4, 2]` is strictly decreasing (`4 > 2`).
- `nums[q...r] = nums[2...3] = [2, 7]` is strictly increasing (`2 < 7`).
- Sum = `1 + 4 + 2 + 7 = 14`.
**Constraints:**

- `4 <= n = nums.length <= 105`
- `109 <= nums[i] <= 109`   
- It is guaranteed that at least one trionic subarray exists.
```java
class Solution {
    long NEG = -100000000000000L;
    //  ↑   ↓   ↑
    // 狀態 s	意義
    // 0	    還沒開始選 subarray
    // 1	    第一段：上升中
    // 2	    第二段：下降中
    // 3	    第三段：最後上升中（完成型）
    public long maxSumTrionic(int[] nums) {
        int n = nums.length;
        // dp[i][s] : 從 index i 開始，在狀態 s 下，能得到的最大總和。
        Long[][] dp = new Long[n + 1][4];

        for (int s = 0; s < 4; s++) {
            // s = 3（已完成三段）
            dp[n][s] = (s == 3) ? 0L : NEG;
        }
        // 1. 不選 nums[i]
        // 2. 選 nums[i]
        for (int i = n - 1; i >= 0; i--) {
            for (int s = 0; s < 4; s++) {
                long take = NEG;
                long notTake = NEG;

                if (s == 0) {// 可以跳過這個元素
                    notTake = dp[i + 1][0];
                }

                if (s == 3) {// 直接把 nums[i] 當作 subarray 的結尾
                    take = nums[i];
                }

                if (i + 1 < n) {
                    if (s == 0 && nums[i + 1] > nums[i]) {// 開始第一段上升
                        take = Math.max(take, nums[i] + dp[i + 1][1]);
                    } else if (s == 1) {// 狀態 1：上升段
                        if (nums[i + 1] > nums[i]) {
                            // 繼續上升
                            take = Math.max(take, nums[i] + dp[i + 1][1]);
                        } else if (nums[i + 1] < nums[i]) {
                            // 進入下降段
                            take = Math.max(take, nums[i] + dp[i + 1][2]);
                        }
                    } else if (s == 2) {// 狀態 2：下降段
                        if (nums[i + 1] < nums[i]) {
                            // 繼續下降
                            take = Math.max(take, nums[i] + dp[i + 1][2]);
                        } else if (nums[i + 1] > nums[i]) {
                            // 開始最後上升
                            take = Math.max(take, nums[i] + dp[i + 1][3]);
                        }
                    } else if (s == 3 && nums[i + 1] > nums[i]) {// 狀態 3：最後上升段（完成型）
                        // 還能繼續上升
                        take = Math.max(take, nums[i] + dp[i + 1][3]);
                    }
                }

                dp[i][s] = Math.max(take, notTake);
            }
        }

        return dp[0][0];
    }
}
```

