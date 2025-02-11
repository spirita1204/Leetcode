# 714. Best Time to Buy and Sell Stock with Transaction Fee

Methods: DP
Difficulty: Medium

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `fee` representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note:**

- You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).
- The transaction fee is only charged once for each stock purchase and sale.

**Example 1:**

```
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.

```

**Example 2:**

```
Input: prices = [1,3,7,5,10,3], fee = 3
Output: 6

```

**Constraints:**

- `1 <= prices.length <= 5 * 104`
- `1 <= prices[i] < 5 * 104`
- `0 <= fee < 5 * 104`

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int hold = Integer.MIN_VALUE / 2 ;// 第一天會持有股票會有問題(無本獲利) 設最小第一天會overflow
        int sold = 0;

        for(int i = 0; i < prices.length; i++) {
            int p = prices[i];// 當天價格
            int preHold = hold;// 避免下面判斷互相改變狀態
            int preSold = sold;

            hold = Math.max(preHold, preSold - p);// 取決於當天不動作 or 今天買入
            sold = Math.max(preSold, p + preHold - fee);// 取決於 當天不動作 or 以今天價格賣出 
        }
        return sold;// 最後依舊持有一定非最大 所以輸出sold
    }
}
```