# 96. Unique Binary Search Trees

Methods: DP
Difficulty: Medium

Given an integer `n`, return *the number of structurally unique **BST'**s (binary search trees) which has exactly* `n` *nodes of unique values from* `1` *to* `n`.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
Input: n = 3
Output: 5

```

**Example 2:**

```
Input: n = 1
Output: 1
```

```java
class Solution {
    public int numTrees(int n) {//dp 取中間root 數量 = 左右子樹 騎術樣相乘後 相加 
        if(n == 1) return 1;
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i++){
            for(int j = 0; j < i; j++){
                dp[i] += dp[j] * dp[i -1 - j];        
            }
        }
        return dp[n];
    }
}
```