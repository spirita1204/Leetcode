# 1052. Grumpy Bookstore Owner

Methods: Sliding Window
Difficulty: Medium

Medium

Topics

Companies

Hint

There is a bookstore owner that has a store open for `n` minutes. Every minute, some number of customers enter the store. You are given an integer array `customers` of length `n` where `customers[i]` is the number of the customer that enters the store at the start of the `ith` minute and all those customers leave after the end of that minute.

On some minutes, the bookstore owner is grumpy. You are given a binary array grumpy where `grumpy[i]` is `1` if the bookstore owner is grumpy during the `ith` minute, and is `0` otherwise.

When the bookstore owner is grumpy, the customers of that minute are not satisfied, otherwise, they are satisfied.

The bookstore owner knows a secret technique to keep themselves not grumpy for `minutes` consecutive minutes, but can only use it once.

Return *the maximum number of customers that can be satisfied throughout the day*.

**Example 1:**

```
Input: customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], minutes = 3
Output: 16
Explanation: The bookstore owner keeps themselves not grumpy for the last 3 minutes.
The maximum number of customers that can be satisfied = 1 + 1 + 1 + 1 + 7 + 5 = 16.

```

**Example 2:**

```
Input: customers = [1], grumpy = [0], minutes = 1
Output: 1

```

**Constraints:**

- `n == customers.length == grumpy.length`
- `1 <= minutes <= n <= 2 * 104`
- `0 <= customers[i] <= 1000`
- `grumpy[i]` is either `0` or `1`.

```java
class Solution {
    public int maxSatisfied(int[] customers, int[] grumpy, int minutes) {
        int length = customers.length;
        int satisfieds = 0;
        int unSatisfieds = 0;
        int makeSatisfieds = 0;// 使滿意區間 - 原本滿意
    
        // cust [1,0,1,2,1,1,7,5]
        // grum [0,1,0,1,0,1,0,1]
        for(int i = 0; i < length; i++) {
            if(grumpy[i] == 0)// 滿意
                satisfieds += customers[i];
            else // 躁怒
                unSatisfieds += customers[i];
            if(i >= minutes && grumpy[i - minutes] == 1) // slide window 後前一個是躁怒 保持固定大小window
                unSatisfieds -= customers[i - minutes];
            // 最大躁怒區間 用minutes
            makeSatisfieds = Math.max(makeSatisfieds, unSatisfieds);
        }
        return satisfieds + makeSatisfieds;
    }
}
```