# 3652. Best Time to Buy and Sell Stock using Strategy  

  Methods: Prefix Sum,Sliding Window </br> Difficulty: Medium </br> </br>You are given two integer arrays `prices` and `strategy`, where:

- `prices[i]` is the price of a given stock on the `ith` day.
- `strategy[i]` represents a trading action on the `ith` day, where:
You are also given an **even** integer `k`, and may perform **at most one** modification to `strategy`. A modification consists of:

- Selecting exactly `k` **consecutive** elements in `strategy`.
- Set the **first** `k / 2` elements to `0` (hold).
- Set the **last** `k / 2` elements to `1` (sell).
The **profit** is defined as the **sum** of `strategy[i] * prices[i]` across all days.

Return the **maximum** possible profit you can achieve.

**Note:** There are no constraints on budget or stock ownership, so all buy and sell operations are feasible regardless of past actions.

**Example 1:**

**Input:** prices = [4,2,8], strategy = [-1,0,1], k = 2

**Output:** 10   

**Explanation:**

Thus, the maximum possible profit is 10, which is achieved by modifying the subarray `[0, 1]`.

**Example 2:**

**Input:** prices = [5,4,3], strategy = [1,1,0], k = 2

**Output:** 9

**Explanation:**

Thus, the maximum possible profit is 9, which is achieved without any modification.

**Constraints:**

- `2 <= prices.length == strategy.length <= 105`
- `1 <= prices[i] <= 105`
- `1 <= strategy[i] <= 1`
- `2 <= k <= prices.length`
- `k` is even
```java
class Solution {
    public long maxProfit(int[] prices, int[] strategy, int k) {
        int n = prices.length, k2 = k / 2;
        long[] prefixSum = new long[n + 1];
        long modify = 0, sum = 0;

        for (int i = 0; i < n; i++) {
            int x = prices[i];
            prefixSum[i + 1] = sum + strategy[i] * x;
            sum += strategy[i] * x;
            modify += ((i >= k2 & i < k) ? x : 0);
        }
        // 修改區間 [0, k-1]
        long profit = Math.max(prefixSum[n], modify + prefixSum[n] - prefixSum[k]);
        // slide windows
        for (int i = 1; i + k <= n; i++) {
            // 保持「只計算後半段 k/2」的效果
            modify += prices[i + k - 1] - prices[i + k2 - 1];
            profit = Math.max(profit, modify + prefixSum[n] - prefixSum[i + k] + prefixSum[i]);
                                              // 全部原始收益 // 扣掉被修改區間原收益
        }
        return profit;
    }
}
```

