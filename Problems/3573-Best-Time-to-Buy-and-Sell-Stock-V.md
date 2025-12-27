# 3573. Best Time to Buy and Sell Stock V  

  Methods: DP </br> Difficulty: Medium++ </br> </br>You are given an integer array `prices` where `prices[i]` is the price of a stock in dollars on the `ith` day, and an integer `k`.

You are allowed to make at most `k` transactions, where each transaction can be either of the following:

- **Normal transaction**: Buy on day `i`, then sell on a later day `j` where `i < j`. You profit `prices[j] - prices[i]`.
- **Short selling transaction**: Sell on day `i`, then buy back on a later day `j` where `i < j`. You profit `prices[i] - prices[j]`.
**Note** that you must complete each transaction before starting another. Additionally, you can't buy or sell on the same day you are selling or buying back as part of a previous transaction.

Return the **maximum** total profit you can earn by making **at most** `k` transactions.

**Example 1:**

**Input:** prices = [1,7,9,8,2], k = 2

**Output:** 14

**Explanation:**

We can make $14 of profit through 2 transactions:

- A normal transaction: buy the stock on day 0 for $1 then sell it on day 2 for $9.
- A short selling transaction: sell the stock on day 3 for $8 then buy back on day 4 for $2.
**Example 2:**

**Input:** prices = [12,16,19,19,8,1,19,13,9], k = 3

**Output:** 36   

**Explanation:**

We can make $36 of profit through 3 transactions:

- A normal transaction: buy the stock on day 0 for $12 then sell it on day 2 for $19.
- A short selling transaction: sell the stock on day 3 for $19 then buy back on day 4 for $8.
- A normal transaction: buy the stock on day 5 for $1 then sell it on day 6 for $19.
**Constraints:**

- `2 <= prices.length <= 103`
- `1 <= prices[i] <= 109`
- `1 <= k <= prices.length / 2`
```java
class Solution {
   public long maximumProfit(int[] prices, int k) {
        // 一次只能持有一個「狀態」
        // 一筆交易一定是 兩步完成
        // 最多 k 筆完整交易
        long ans = 0;
        int n = prices.length;
        // dp[i][k][decider]
        // i	第 i 天
        // k	剩餘可完成的「交易數」
        // decider	當前狀態
        
        // decider	意義
        // 0	空手（沒有持倉）
        // 1	持有 多單（已買，等賣）
        // 2	持有 空單（已賣，等買回）
        Long[][][] dp = new Long[n][k + 1][3];
        long res = solve(0, k, 0, prices, dp);
        return res;
    }

    long solve(int i, int k, int decider, int[] prices, Long[][][] dp) {
        if (i == prices.length) {
            if (k >= 0 && decider == 0)
                return 0;// 如果是 空手狀態 → 合法結束，收益 0
            return Integer.MIN_VALUE;// 如果還持倉（多單或空單）→ 非法 → 給極小值避免選到
        }

        if (dp[i][k][decider] != null) {
            return dp[i][k][decider];// memorize
        }
        // 今天動作                     // 今天什麼都不做
        long take = Integer.MIN_VALUE, dontTake = Integer.MIN_VALUE;
        if (k > 0) {
            if (decider == 1) { // 1	持有 多單（已買，等賣）
                take = prices[i] + solve(i + 1, k - 1, 0, prices, dp);
            } else if (decider == 2) { // 買回 → 完成一筆交易
                take = -prices[i] + solve(i + 1, k - 1, 0, prices, dp);
            } else {
                                // 開空單（先賣）
                take = Math.max(prices[i] + solve(i + 1, k, 2, prices, dp),
                        // 開多單（買入）
                        -prices[i] + solve(i + 1, k, 1, prices, dp));
            }
        }

        dontTake = solve(i + 1, k, decider, prices, dp);
        return dp[i][k][decider] = Math.max(take, dontTake);
    }
}
```

