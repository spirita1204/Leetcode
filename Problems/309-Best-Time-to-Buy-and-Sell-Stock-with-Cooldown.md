# 309. Best Time to Buy and Sell Stock with Cooldown

Methods: DP
Difficulty: Medium

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

- After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]

```

**Example 2:**

```
Input: prices = [1]
Output: 0
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 三種狀態
        // hold = max[hold, cooled - p] 前天不能是剛賣 所以是cooled - p
        // sold = [p + hold] 
        // cooled = [cooled, sold] 昨天剛賣掉
        // 剛賣完叫sold 賣完兩天叫cooled
        int hold = Integer.MIN_VALUE;
        int sold = 0;
        int cooled = 0;
        for(int i = 0; i < prices.length; i++) {
            int p = prices[i];// 當天價格
            int preHold = hold;// 避免下面判斷互相改變狀態
            int preSold = sold;
            int preCooled = cooled;
            
            hold = Math.max(preHold, preCooled - p);// 取決於當天不動作 or 今天買入
            sold =  p + preHold;// 以今天價格賣出 
            cooled = Math.max(cooled, preSold);
        }
        return Math.max(sold, cooled);
    }
}
```