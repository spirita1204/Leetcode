# 322. Coin Change (經典題)

Methods: DP
Difficulty: Medium

**Medium**

16.1K

366

Companies

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the fewest number of coins that you need to make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1

```

**Example 3:**

```
Input: coins = [1], amount = 0
Output: 0

```

**Constraints:**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`

```java
class Solution {
    public int coinChange(int[] coins, int amount) {// 滾動數組 降維
        // not Greedy problem
        // int[][] dp = new int[amount+ 1];// 使用第i之前所有coins可以組成之j Amount
        // dp[i][j] = min(dp[i][j], dp[i][j - coins_i] + 1)
        int[] dp = new int[amount + 1]; // min coins to make up to amount 滾動數組
        Arrays.fill(dp, amount + 1);// 給定無限大 但不能Integer.MAX_VALUE 因為加1會溢位
        dp[0] = 0;

        for(int coin: coins){
            for(int i = coin; i<= amount; i++){
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }

        return dp[amount] >= amount + 1 ? -1 : dp[amount];
    }
}
```

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        // not Greedy problem
        // https://www.youtube.com/watch?v=uUETHdijzkA&t=524s
        int[][] dp = new int[coins.length + 1][amount + 1];// 使用第i之前所有coins可以組成之j Amount

        Arrays.fill(dp[0], amount + 1);// 給定無限大 但不能Integer.MAX_VALUE 因為加1會溢位

        for(int i = 1; i<= coins.length; i++){
            for(int j = 1; j<= amount; j++){
                if(j < coins[i - 1]) dp[i][j] = dp[i-1][j];// 將上一欄資料帶入
                else dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - coins[i - 1]] + 1);
            }
        }

        return dp[coins.length][amount] >= amount + 1 ? -1 : dp[coins.length][amount];
    }
}
```