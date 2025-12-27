# 3578. Count Partitions With Max-Min Difference at Most K  

  Methods: Prefix Sum,DP,Sliding Window </br> Difficulty: Medium,Medium++ </br> </br>You are given an integer array `nums` and an integer `k`. Your task is to partition `nums` into one or more **non-empty** contiguous segments such that in each segment, the difference between its **maximum** and **minimum** elements is **at most** `k`.

Return the total number of ways to partition `nums` under this condition.

Since the answer may be too large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** nums = [9,4,1,3,7], k = 4

**Output:** 6

**Explanation:**

There are 6 valid partitions where the difference between the maximum and minimum elements in each segment is at most `k = 4`:

- `[[9], [4], [1], [3], [7]]`
- `[[9], [4], [1], [3, 7]]`
- `[[9], [4], [1, 3], [7]]`
- `[[9], [4, 1], [3], [7]]`
- `[[9], [4, 1], [3, 7]]`
- `[[9], [4, 1, 3], [7]]`
**Example 2:**

**Input:** nums = [3,3,4], k = 0

**Output:** 2

**Explanation:**

There are 2 valid partitions that satisfy the given conditions:

- `[[3], [3], [4]]`     
- `[[3, 3], [4]]`    
**Constraints:**

- `2 <= nums.length <= 5 * 104`
- `1 <= nums[i] <= 109`
- `0 <= k <= 109`
```java
class Solution {
    public int countPartitions(int[] nums, int k) {
        int n = nums.length;
        long mod = 1_000_000_007L;
        // dp[i]：表示前 i 個元素（nums[0..i-1] 的合法切割方式數
        long[] dp = new long[n + 1];
        long[] prefix = new long[n + 1];
        TreeMap<Integer, Integer> cnt = new TreeMap<>();

        dp[0] = prefix[0] = 1;
        int j = 0;// 左指標

        for (int i = 0; i < n; i++) {
            // 將 nums[i] 加入目前視窗
            cnt.put(nums[i], cnt.getOrDefault(nums[i], 0) + 1);
            // 用滑動視窗維護「max - min ≤ k」的最左合法起點 j，
            // 若視窗內 max - min > k
            // 則持續右移 j，直到合法
            while (cnt.lastKey() - cnt.firstKey() > k) {
                int val = nums[j];
                int c = cnt.get(val) - 1;

                if (c == 0)
                    cnt.remove(val);
                else
                    cnt.put(val, c);

                j++;
            }
            // 此時 [j .. i] 是「最左邊合法」的區間
            // dp[i+1] = dp[j] + dp[j+1] + ... + dp[i]
            // 利用 prefix sum 快速計算
            long left = (j > 0 ? prefix[j - 1] : 0);
            dp[i + 1] = (prefix[i] - left + mod) % mod;// dp[j] + ... + dp[i] = prefix[i] - prefix[j-1]
            // prefix[i]：dp[0] + dp[1] + ... + dp[i]
            // 用來快速計算區間 dp 總和
            prefix[i + 1] = (prefix[i] + dp[i + 1]) % mod;
        }

        return (int) dp[n];
    }
}

```

