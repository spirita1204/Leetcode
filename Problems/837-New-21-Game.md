# 837. New 21 Game  

  Methods: Math,DP,Sliding Window </br> Difficulty: Medium </br> </br>Alice plays the following game, loosely based on the card game **"21"**.

Alice starts with `0` points and draws numbers while she has less than `k` points. During each draw, she gains an integer number of points randomly from the range `[1, maxPts]`, where `maxPts` is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets `k` **or more points**.

Return the probability that Alice has `n` or fewer points.

Answers within `10-5` of the actual answer are considered accepted.

**Example 1:**

```plain text
Input: n = 10, k = 1, maxPts = 10
Output: 1.00000
Explanation: Alice gets a single card, then stops.
```

**Example 2:**

```plain text
Input: n = 6, k = 1, maxPts = 10
Output: 0.60000
Explanation: Alice gets a single card, then stops.
In 6 out of 10 possibilities, she is at or below 6 points.
```

**Example 3:**

```plain text
Input: n = 21, k = 17, maxPts = 10
Output: 0.73278
```

**Constraints:**

- `0 <= k <= n <= 104`
- `1 <= maxPts <= 104`
```java
class Solution {
    public double new21Game(int N, int K, int maxPts) {
        if (K == 0 || N >= K - 1 + maxPts) return 1.0;// 0 || 最後一抽抽到最大值，也不會超過 N
        // 最後的分數一定在：[K, K + maxPts - 1]
        double[] dp = new double[maxPts]; // dp[i] = 剛好到達分數 i 的機率
        dp[0] = 1.0;
        // dp[i] = (dp[i-1] + dp[i-2] + ... + dp[i-maxPts]) / maxPts 每個點跳過去機率都依樣
        double windowSum = 1.0, result = 0.0;
        // windowSum = dp[i-1] + dp[i-2] + ... + dp[i-maxPts]
        // dp[i] = windowSum / maxPts;
        for (int i = 1; i <= N; i++) {
            double prob = windowSum / maxPts;
            
            if (i < K) {// 還能繼續往後貢獻 
                windowSum += prob;
            } else {// dp[i] 是「最終結果」 累加到答案
                result += prob;
            }

            if (i >= maxPts) {
                windowSum -= dp[i % maxPts];
            }
            // 把「太舊」的 dp[i-maxPts] 移出視窗
            dp[i % maxPts] = prob;
        }

        return result;
    }
}
```

