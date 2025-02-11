# 2218. Maximum Value of K Coins From Piles

Methods: DP
Difficulty: Hard

**Hard**

1.2K

17

Companies

There are `n` **piles** of coins on a table. Each pile consists of a **positive number** of coins of assorted denominations.

In one move, you can choose any coin on **top** of any pile, remove it, and add it to your wallet.

Given a list `piles`, where `piles[i]` is a list of integers denoting the composition of the `ith` pile from **top to bottom**, and a positive integer `k`, return *the **maximum total value** of coins you can have in your wallet if you choose **exactly*** `k` *coins optimally*.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/11/09/e1.png](https://assets.leetcode.com/uploads/2019/11/09/e1.png)

```
Input: piles = [[1,100,3],[7,8,9]], k = 2
Output: 101
Explanation:
The above diagram shows the different ways we can choose k coins.
The maximum total we can obtain is 101.

```

**Example 2:**

```
Input: piles = [[100],[100],[100],[100],[100],[100],[1,1,1,1,1,1,700]], k = 7
Output: 706
Explanation:
The maximum total can be obtained if we choose all coins from the last pile.

```

**Constraints:**

- `n == piles.length`
- `1 <= n <= 1000`
- `1 <= piles[i][j] <= 105`
- `1 <= k <= sum(piles[i].length) <= 2000`

![Untitled](Untitled%2014.png)

```jsx
class Solution {
    public int maxValueOfCoins(List<List<Integer>> piles, int k) {
        //令 dp[i][j] = 從第0堆到第i堆取j個
        // dp[i][j] = max( dp[i-1][j-t] + pile[i][t] ) 當前等於到前i-1堆取出j-t + 第i堆拿t 
        int[][] dp = new int[piles.size()+1][k+1];//避免第行溢位
        int[][] eachPiles = new int[piles.size()+1][k+1];

        int i = 1;//記錄第幾堆 
        for(List<Integer> sub : piles){
            int j = 1;// 第i堆取幾j個
            for(int a : sub){
                if(j > k) break;
                eachPiles[i][j] += a + eachPiles[i][j-1];
                j++;
            }
            i++;
        }

        for(int p1 = 1; p1< piles.size()+1; p1++){// x座標 第幾堆
            for(int p2 = 1; p2< k+1; p2++){// y座標 取幾個
                for(int n = 0; n< k+ 1; n++){// 所有可以拿取組合
                    if(p2 - n < 0) break;// 
                    dp[p1][p2] = Math.max(dp[p1][p2], dp[p1-1][p2-n] + eachPiles[p1][n]);
                }
            }
        }
        return dp[piles.size()][k];
    }
}
```