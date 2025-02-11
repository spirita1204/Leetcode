# 121. Best Time to Buy and Sell Stock

Methods: Basic logic
Difficulty: Easy

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

```

**Example 2:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        //找最大 和最小 最小需再最大前
        int profit = 0;//最大利潤
        int min = Integer.MAX_VALUE;//最小
        for(int i = 0 ; i < prices.length ; i++){
            if(prices[i] < min) min = prices[i];
            if(profit < prices[i] - min) profit = prices[i] - min;
        }
        return profit;
    }
}
```