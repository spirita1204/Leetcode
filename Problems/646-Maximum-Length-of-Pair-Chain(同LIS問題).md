# 646. Maximum Length of Pair Chain(同LIS問題)

Methods: DP
Difficulty: Medium

Medium

Topics

Companies

You are given an array of `n` pairs `pairs` where `pairs[i] = [lefti, righti]` and `lefti < righti`.

A pair `p2 = [c, d]` **follows** a pair `p1 = [a, b]` if `b < c`. A **chain** of pairs can be formed in this fashion.

Return *the length longest chain which can be formed*.

You do not need to use up all the given intervals. You can select pairs in any order.

**Example 1:**

```
Input: pairs = [[1,2],[2,3],[3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4].

```

**Example 2:**

```
Input: pairs = [[1,2],[7,8],[4,5]]
Output: 3
Explanation: The longest chain is [1,2] -> [4,5] -> [7,8].

```

**Constraints:**

- `n == pairs.length`
- `1 <= n <= 1000`
- `1000 <= lefti < righti <= 1000`

```java
class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[0] - b[0]);// 先根據index 0 做排序
        int[] dp = new int[pairs.length];
        dp[0] = 1;

        for(int i = 1 ; i < pairs.length; i++){
            int max = Integer.MIN_VALUE;
            for(int k = i - 1 ; k >= 0 ; k--){
                if(pairs[k][0] < pairs[i][0] && pairs[k][1] < pairs[i][0]){//當 遞增
                    max = Math.max(max,dp[k]);
                }
            }
            dp[i] = (max == Integer.MIN_VALUE) ? 1 : max + 1; //當前節點為上一段最常節點+1
        }   
        Arrays.sort(dp);
        return dp[pairs.length - 1];
    }
}
```