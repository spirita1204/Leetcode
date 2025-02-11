# 123. Best Time to Buy and Sell Stock III

Methods: DP
Difficulty: Hard

**Hard**

8.1K

157

Companies

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

**Example 2:**

```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.

```

**Example 3:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

```

**Constraints:**

- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 105`

```java
class Solution {
    public int maxProfit(int[] prices) {
        /** 四種狀態
            第i-1輪           持有第一股  售出第一股  持有第二股  售出第二股
                                |    \      |    \     |   \      | 
                                | + val[i]  |  -val[i] |  +val[i] |
                                v       \   v       \  v      \   v
            第 i 輪  -val[i]  持有第一股  售出第一股  持有第二股  臭出第二股

            0:這輪我已持有第一股的最大收益
            1:這輪我已售出第一股的最大收益
            2:這輪我已持有第二股的最大收益
            3:這輪我已售出第二股的最大收益
         */
        
        // 第i天的第幾種狀態(4種)
        int buy1 = Integer.MIN_VALUE;
        int buy2 = Integer.MIN_VALUE;
        int sold1 = 0;
        int sold2 = 0;
        
        for(int i = 1; i<= prices.length; i++){
            //                  維持   交易
            buy1 = Math.max(buy1, -prices[i-1]);
            sold1 = Math.max(sold1, buy1 + prices[i-1]); 
            buy2 = Math.max(buy2, sold1 - prices[i-1]); 
            sold2 = Math.max(sold2, buy2 + prices[i-1]); 
        }
   
        // 更進一步可以只輸出1,3 其中之一最大
        return Math.max(buy1, Math.max(buy2, Math.max(sold1, sold2)));
    }
}
```