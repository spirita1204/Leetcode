# 494. Target Sum

Methods: DP
Difficulty: Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3

```

**Example 2:**

```
Input: nums = [1], target = 1
Output: 1

```

**Constraints:**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `1000 <= target <= 1000`

DFS

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        return dfs(nums, target, 0, 0);
    }
    public int dfs(int[] nums, int target, int pointer, int sum){
        if(pointer >= nums.length && sum == target) return 1;  
        if(pointer >= nums.length && sum != target) return 0;

        int addCount = dfs(nums, target, pointer + 1, sum + nums[pointer]);
        int subCount = dfs(nums, target, pointer + 1, sum - nums[pointer]);

        return addCount + subCount;
    }
}
```

DP最優解 

[花花酱 LeetCode 494. Target Sum 上 - 刷题找工作 EP156](https://www.youtube.com/watch?v=r6Wz4W1TbuI&t=356s)

![Untitled](Untitled%202.png)

![Untitled](Untitled%203.png)

![Untitled](Untitled%204.png)

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        return dp(nums, target);
    }
    public int dp(int[] nums, int target){//ways[i][j] # of ways to sum up to j using nums[0~i] 
        //             = ways[i - 1][j - nums[i]] + ways[i - 1][j - nums[i]]
        //init : ways[-1][0] = 1 無任何樹構成0 是ok的
        //ans : ways[m - 1][s]
        int sum = 0;
        for(int i : nums){
            sum += i;
        }
        int ways[][] = new int[nums.length + 1][sum*2+1];
        ways[0][sum] = 1;
        for(int i = 1; i <= nums.length; i++){
            for(int j = 0; j < sum*2+1; j++){
                if(j - nums[i - 1] < 0) ways[i][j] = ways[i - 1][j + nums[i - 1]];
                else if(j + nums[i - 1]  > sum*2) ways[i][j] = ways[i - 1][j - nums[i - 1]];
                else ways[i][j] = ways[i - 1][j - nums[i - 1]] + ways[i - 1][j + nums[i - 1]];
            }
        }
        return (target > sum || target < -sum) ? 0 : ways[nums.length][sum+target];
    }
}
```