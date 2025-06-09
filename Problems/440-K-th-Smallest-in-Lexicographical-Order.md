# 440. K-th Smallest in Lexicographical Order  

  Data Structure: Trie </br> Difficulty: Hard </br> </br>Given two integers `n` and `k`, return *the* `kth` *lexicographically smallest integer in the range* `[1, n]`.

**Example 1:**

```plain text
Input: n = 13, k = 2
Output: 10
Explanation: The lexicographical order is [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9], so the second smallest number is 10.
```

**Example 2:**

```plain text
Input: n = 1, k = 1
Output: 1
```

**Constraints:**

- `1 <= k <= n <= 109`
```java
class Solution {
    public int findKthNumber(int n, int k) {
        long curr = 1; // Start from the prefix 1
        k--; // We start counting from 1, so decrement k
        // 1 11 12 13 14 111..
        // 2 21 22 222...
        while (k > 0) {
            long steps = countSteps(curr, n);
            if (steps <= k) {// 遍歷prefix 1->2
                curr++; // Move to the next prefix
                k -= steps;
            } else {// 1 -> 遍歷10 11 12..
                curr *= 10; // Dive deeper into the current prefix
                k--;
            }
        }
        return (int) curr;
    }

    // Helper function to count the steps within the range [curr, n].
    private long countSteps(long curr, long n) {// 1 13 -> 1 10 11 12 13(五個)
        long steps = 0, first = curr, last = curr;// 1 1
        while (first <= n) {
            steps += Math.min(n + 1, last + 1) - first;
            first *= 10;// 10
            last = last * 10 + 9;// 19
        }
        return steps;
    }
}
```

