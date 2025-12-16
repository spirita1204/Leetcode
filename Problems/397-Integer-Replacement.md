# 397. Integer Replacement  

  Methods: DFS </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

Given a positive integer `n`, you can apply one of the following operations:

1. If `n` is even, replace `n` with `n / 2`.
1. If `n` is odd, replace `n` with either `n + 1` or `n - 1`.
Return *the minimum number of operations needed for* `n` *to become* `1`.

**Example 1:**

```plain text
Input: n = 8
Output: 3
Explanation: 8 -> 4 -> 2 -> 1

```

**Example 2:**

```plain text
Input: n = 7
Output: 4
Explanation:7 -> 8 -> 4 -> 2 -> 1
or 7 -> 6 -> 3 -> 2 -> 1

```

**Example 3:**

```plain text
Input: n = 4
Output: 2

```

**Constraints:**

- `1 <= n <= 231 - 1`
```java
class Solution {
    int sum = Integer.MAX_VALUE;

    public int integerReplacement(int n) {
        recursion(n, 0);
        return sum;
    }

    private void recursion(long n, int step) {// MAX_VALUE時 往上可以少走一步
        if (n == 1) {
            sum = Math.min(sum, step);
            return;
        }
        if (n % 2 == 0) {// 偶數
            recursion(n / 2, step + 1);
        } else {// 奇數
            recursion(n + 1, step + 1);
            recursion(n - 1, step + 1);
        }
    }
}
```

