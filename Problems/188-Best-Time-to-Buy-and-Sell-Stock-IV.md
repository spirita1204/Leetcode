# 188. Best Time to Buy and Sell Stock IV

Methods: DP
Difficulty: Hard

Hard

Topics

Companies

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions: i.e. you may buy at most `k` times and sell at most `k` times.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.

```

**Example 2:**

```
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.

```

**Constraints:**

- `1 <= k <= 100`
- `1 <= prices.length <= 1000`
- `0 <= prices[i] <= 1000`

```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        // 第i天的第幾種狀態(k種)
        int[][] state = new int[2][k];
        Arrays.fill(state[0], Integer.MIN_VALUE);
        /** ___________________________________
            |__________________________________| buy
            |__________________________________| sold
         */
        for(int i = 0; i < prices.length; i++) {
            //                  維持   交易
            for(int j = 0; j < state[0].length; j++) {
                if(j == 0) {
                    state[0][j] = Math.max(state[0][j], -prices[i]);
                    state[1][j] = Math.max(state[1][j], state[0][j] + prices[i]); 
                } else {
                    state[0][j] = Math.max(state[0][j], state[1][j - 1] - prices[i]);
                    state[1][j] = Math.max(state[1][j], state[0][j] + prices[i]); 
                }
            }
            // buy1 = Math.max(buy1, -prices[i]);
            // sold1 = Math.max(sold1, buy1 + prices[i]); 
            // buy2 = Math.max(buy2, sold1 - prices[i]); 
            // sold2 = Math.max(sold2, buy2 + prices[i]); 
        }
        Arrays.sort(state[1]);
        return state[1][state[0].length - 1];
    }
}
```