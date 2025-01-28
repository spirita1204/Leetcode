# 45. Jump Game II

Methods: DP, Greedy
Difficulty: Medium

**Medium**

12.1K

422

Companies

You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

- `0 <= j <= nums[i]` and
- `i + j < n`

Return *the minimum number of jumps to reach* `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

```

**Example 2:**

```
Input: nums = [2,3,0,1,4]
Output: 2

```

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- It's guaranteed that you can reach `nums[n - 1]`.

### Greedy

```java
class Solution {
    public int jump(int[] nums) {
        int res = 0;// 步數
        int max = 0;// 可走到最遠距離
        int curr = max;
        // greedy法 找每次能到達最遠 計次->當到達終點即為所需次數
        for(int i = 0; i< nums.length; i++){
            if(i > curr){
                res++;
                curr = max;
            }
            max = Math.max(max, i + nums[i]);
        }
        return res;
    }
}
```

## DP

```java
class Solution {
    public int jump(int[] nums) {
        int len = nums.length;
        int[] dp = new int[len];

        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for(int i = 0; i < len; i++) {
            for(int j = i; j <= i + nums[i] && j < len; j++) {
                dp[j] = Math.min(dp[j], dp[i] + 1);
            }
        }
        return dp[len - 1];
    }
}
```