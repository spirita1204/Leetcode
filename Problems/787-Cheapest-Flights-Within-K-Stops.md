# 787. Cheapest Flights Within K Stops

Methods: DP
Difficulty: Medium

[https://youtu.be/5V_72xBSh8E](https://youtu.be/5V_72xBSh8E)

# **Intuition**

Credit to @gcl272633743

![https://assets.leetcode.com/users/images/f9e5e5c9-161e-47f6-ab9f-44c5eb9bc735_1674696379.0685956.png](https://assets.leetcode.com/users/images/f9e5e5c9-161e-47f6-ab9f-44c5eb9bc735_1674696379.0685956.png)

We will have a table where columns are cities and row indicates steps(not stops) Any row, column indicates cost to travel from src to this city in k steps. If its infinity its not possible.

Initially all are infinity, we mark the source column to 0, as the cost required to travel from src to src is 0 with any steps.

Now we go to each step, i.e say step 1 (row 1).

We check all the flights and if the source is already visited, i.e(the previous row is not infinity) we change this cell's value.

ex [0,1,100] city 0 is visisted with 0 steps, hence dp[1][1] = 100;[1,2,100] no change since 1 is not visited in previous steps.

Same goes for 2 stepseg [1,2,100]-- is 1 already visited, yes so dp[2][2] = 100+100[1,3,600] -- is 1 already visited, yes dp[2][3] = 100+600 =700

For More read: [https://medium.com/swlh/graph-dynamic-programming-heap-cheapest-flights-within-k-stops-e622ce956479](https://medium.com/swlh/graph-dynamic-programming-heap-cheapest-flights-within-k-stops-e622ce956479)

# **Approach**

# **Complexity**

- Time complexity:
- Space complexity:

# **Code**

```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        int[][] dp = new int[k+2][n];
        for(int i=0; i<=k+1; i++){
            Arrays.fill(dp[i],Integer.MAX_VALUE);    
        }
        //fly from src to scr cost 0
        for(int i=0; i<=k+1; i++){
            dp[i][src] = 0;    
        }
        
        for(int i=1; i<=k+1; i++){
            for(int[] f: flights){
                if(dp[i-1][f[0]]!=Integer.MAX_VALUE){
                    dp[i][f[1]] = Math.min(dp[i][f[1]],dp[i-1][f[0]]+f[2]);
                }
            }
        }
        return dp[k+1][dst] == Integer.MAX_VALUE ? -1 : dp[k+1][dst];
    }
}
```

[[演算法] 最短路徑 (Bellman-Ford 演算法) - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10209748)