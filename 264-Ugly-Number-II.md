# 264. Ugly Number II

Methods: DP
Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

Hint

An **ugly number** is a positive integer whose prime factors are limited to `2`, `3`, and `5`.

Given an integer `n`, return *the* `nth` ***ugly number***.

**Example 1:**

```
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.

```

**Example 2:**

```
Input: n = 1
Output: 1
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.

```

**Constraints:**

- `1 <= n <= 1690`

---

---

---

---

Hint 1

The naive approach is to call `isUgly` for every number until you reach the nth one. Most numbers are *not* ugly. Try to focus your effort on generating only the ugly ones.

---

Hint 2

An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.

---

Hint 3

The key is how to maintain the order of the ugly numbers. Try a similar approach of merging from three sorted lists: L1, L2, and L3.

---

Hint 4

Assume you have Uk, the kth ugly number. Then Uk+1 must be Min(L1 * 2, L2 * 3, L3 * 5).

### Heap

Runtime

msBeats **5.05%**

---

Memory

MBBeats **17.43%**

```java
class Solution {
    public int nthUglyNumber(int n) {
        // min(2, 3, 5) 1*2, 1*3, 1*5 -> 1 -> 2,3,5 -> 4,6,10 -> 6
        Queue<Long> pq = new PriorityQueue<>();
        pq.offer(1L);
        long number = 1L;
        for(int i = 0; i < n; i++) {
            number = pq.poll();
            if(!pq.contains(number* 2) && number* 2 > 0)// 避免易位
                pq.offer(number* 2);
            if(!pq.contains(number* 3) && number* 3 > 0)
                pq.offer(number* 3);
            if(!pq.contains(number* 5) && number* 5 > 0)
                pq.offer(number* 5);
        }
        return (int)number;
    }
}
```

---

### DP

```jsx
class Solution {
    public int nthUglyNumber(int n) {
        // DP
        int t2 = 0, t3 = 0, t5 = 0; //pointers for 2, 3, 5
        int[] dp = new int[n];
        dp[0] = 1;
        for(int i = 1; i < n ; i ++) {
            dp[i] = Math.min(dp[t2] * 2, Math.min(dp[t3] * 3, dp[t5] * 5));
            if(dp[i] == dp[t2] * 2) t2++; 
            if(dp[i] == dp[t3] * 3) t3++;
            if(dp[i] == dp[t5] * 5) t5++;
        }
        return dp[n-1];
    }
}
```