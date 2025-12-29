# 808. Soup Servings  

  Methods: Math,DP </br> Difficulty: Medium </br> </br>You have two soups, **A** and **B**, each starting with `n` mL. On every turn, one of the following four serving operations is chosen *at random*, each with probability `0.25` **independent** of all previous turns:

- pour 100 mL from type A and 0 mL from type B
- pour 75 mL from type A and 25 mL from type B
- pour 50 mL from type A and 50 mL from type B
- pour 25 mL from type A and 75 mL from type B
**Note:**

- There is no operation that pours 0 mL from A and 100 mL from B.
- The amounts from A and B are poured *simultaneously* during the turn.
- If an operation asks you to pour **more than** you have left of a soup, pour all that remains of that soup.
The process stops immediately after any turn in which *one of the soups* is used up.

Return the probability that A is used up *before* B, plus half the probability that both soups are used up in the** same turn**. Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

```plain text
Input: n = 50
Output: 0.62500
Explanation:
If we perform either of the first two serving operations, soup A will become empty first.
If we perform the third operation, A and B will become empty at the same time.
If we perform the fourth operation, B will become empty first.
So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.25 * (1 + 1 + 0.5 + 0) = 0.625.
```

**Example 2:**

```plain text
Input: n = 100
Output: 0.71875
Explanation:
If we perform the first serving operation, soup A will become empty first.
If we perform the second serving operations, A will become empty on performing operation [1, 2, 3], and both A and B become empty on performing operation 4.
If we perform the third operation, A will become empty on performing operation [1, 2], and both A and B become empty on performing operation 3.
If we perform the fourth operation, A will become empty on performing operation 1, and both A and B become empty on performing operation 2.
So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.71875.
```

**Constraints:**

- `0 <= n <= 109`
```java
class Solution {
    // dp[a][b] = 當 A 剩 a 單位、B 剩 b 單位時，最終符合題目條件的機率
    private Double[][] memo;
    // P(A 先用完) + 0.5 × P(A、B 同時用完)
    public double soupServings(int n) {
        if (n == 0) return 0.5;
        // 當 n 足夠大，P(A 先空) → 1 證明的
        if (n >= 4800) return 1.0;
        // 只要剩不到 25 mL，也會在下一次被倒光
        int N = (n + 24) / 25; // ceil
        memo = new Double[N + 1][N + 1];
        return dfs(N, N);
    }

    private double dfs(int a, int b) {
        if (a <= 0 && b <= 0) return 0.5;// 同時用完
        if (a <= 0) return 1.0;// A 明確比 B 先用完
        if (b <= 0) return 0.0;// B 先用完

        if (memo[a][b] != null) return memo[a][b];
        // 四種操作，每種機率 0.25：
        memo[a][b] = 0.25 * (
            dfs(a - 4, b) +
            dfs(a - 3, b - 1) +
            dfs(a - 2, b - 2) +
            dfs(a - 1, b - 3)
        );
        return memo[a][b];
    }
}

```

