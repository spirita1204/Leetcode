# 790. Domino and Tromino Tiling  

  Methods: DP </br> Difficulty: Medium </br> </br>![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/551e162b-3aee-4da0-b433-c68d9d5b2536/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TH3WJPZP%2F20250505%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250505T135315Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCc%2Fw7t9yQlc4UR94jd%2BEL9ZZBVkqdbLGk7vT0WifSHCQIgIqv9x9%2BhAoxRrAjzD4wiIN7RghrNSkT2RW7hvQrbz%2BUq%2FwMILxAAGgw2Mzc0MjMxODM4MDUiDMDDFr7z6ZWCZcgzECrcA0MiILoLa3zqFkEI5wLLk9oag9UEP3Ekt3qHp5nd3%2Fh18NOWP79B%2Byslh9iy4D3TNvo59JtRQOvSQ7Uc5VQvFRH%2F%2FlJjN2AnDqJRSMh4%2FJfhBNVar6rFEuSXxPhz1jhkQErTYrq8c7bmSpyyHLUb2j%2BxV3iV1sUWnt4QZWFnt3hC3JXxr4QBVIdvKraereqaKNbv1E7BxtKiM2ep%2B2KiUhIu4DuZ8ythNjPlBnGQBDzw2pgxUtqjTJYtqbTdYb0Q2EwFbsNJETNgofhBqmdKX4TErjJdUZXrNZv%2FPyJMXWzRvJ1ZUcy7C0lzEBoFSXcRFDsXLrh4w6OtvwwnPzn83oylURkK6RQAiQZGQT5tx4yAkKc%2B%2B5dBAarTbjFrXE7%2F3TPFBaHcJC1ao%2BeBHu8CFFWjUK8L6pxePRsoHLEJKdjlYt7oO2z2ps2lWarS53%2BjFR03mPw9aXGFqJZnMg%2BR5Dj1Ska4%2FS16qLZprgxcKQRpqO0y2HBPKLPgvb7zRj3cLQsi5OOgSrp5vuPmNz8PFQ3LNR%2FJ79Vk4uH3rT8GiLvskujGD9ID%2BgpZMP1smAezkBOzsXjWw5L74v9nx97xf2ABKXMkff8VijJSDmaTrsnUIgPSuTiqPdd7OtRcMOr%2B4sAGOqUBVScXckqU67AQ6fwtgD6YIjK7HuoC1x0M59%2BRcpkT%2FqvMTXhFljQxJzEQYuCA8%2F9ueMLE5wTYrYZI3rh3A9cQykjlLvAMuTgCDITBFJpFxS7bbYKZJJf2UPH1Y%2FRFrV0Q0PjdFPmMcZfW0yD1ImOCh6I53cU8V4XoEOBx87YamlKgOyvFuMywD2IA7Dpp7uRg34yZiVfYSzecpuyU7WbVhaoZf5HH&X-Amz-Signature=8cef66b2149662f5e34a8ef0d883cf62a17faa7e34ea1b43b37b4d460acee75d&X-Amz-SignedHeaders=host&x-id=GetObject)

You have two types of tiles: a `2 x 1` domino shape and a tromino shape. You may rotate these shapes.

![Image](https://assets.leetcode.com/uploads/2021/07/15/lc-domino.jpg)

Given an integer n, return *the number of ways to tile an* `2 x n` *board*. Since the answer may be very large, return it **modulo** `109 + 7`.

In a tiling, every square must be covered by a tile. Two tilings are different if and only if there are two 4-directionally adjacent cells on the board such that exactly one of the tilings has both squares occupied by a tile.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/07/15/lc-domino1.jpg)

```plain text
Input: n = 3
Output: 5
Explanation: The five different ways are show above.
```

**Example 2:**

```plain text
Input: n = 1
Output: 1
```

**Constraints:**

- `1 <= n <= 1000`
```java
class Solution {
    public int numTilings(int n) {
        int mod = 1000000007;
        long[][] dp = new long[n + 1][2];
        dp[0][0] = 1;
        dp[1][0] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i][0] = (dp[i - 1][0] + dp[i - 2][0] + 2 * dp[i - 1][1] % mod) % mod;
            dp[i][1] = (dp[i - 2][0] + dp[i - 1][1]) % mod;
        }
        return (int)dp[n][0];
    }
}
```



