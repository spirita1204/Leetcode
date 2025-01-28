# 300. Longest Increasing Subsequence(經典題)

Methods: DP
Difficulty: Medium

Given an integer array `nums`, return *the length of the longest **strictly increasing subsequence***.

**Example 1:**

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

```

**Example 2:**

```
Input: nums = [0,1,0,3,2,3]
Output: 4

```

**Example 3:**

```
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

```java
class Solution {
    public int lengthOfLIS(int[] nums) {//DP O(n^2)
        int[] dp = new int[nums.length];
        dp[0] = 1;
        for(int i = 1 ; i < nums.length ; i++){
            int max = Integer.MIN_VALUE;
            for(int k = i - 1 ; k >= 0 ; k--){
                if(nums[k] < nums[i]){//當 遞增
                    max = Math.max(max,dp[k]);
                }
            }
            dp[i] = (max == Integer.MIN_VALUE) ? 1 : max + 1; //當前節點為上一段最常節點+1
        }   
        Arrays.sort(dp);
        return dp[nums.length - 1];
    }

    public int lengthOfLIS(int[] nums) {//DP O(n*log(n))
			int[] tails = new int[nums.length];//紀錄不同長度下末端最優解
			int size = 0;

			for (int x : nums) {
					int left = 0, right = size;
					while (left < right) {
							int m = (left + right) / 2;
							if (tails[m] < x)//往後延伸
									left = m + 1;
							else
									right = m;//當比較小 可以以它作為結尾 更優解
					}
					tails[left] = x;
					if (left == size) ++size;
			}
			return size;        
    }
}
```

可優化如下O(n log n)

[https://www.youtube.com/watch?v=l2rCz7skAlk](https://www.youtube.com/watch?v=l2rCz7skAlk)

O(n^2)

[https://www.youtube.com/watch?v=7DKFpWnaxLI&ab_channel=HuaHua](https://www.youtube.com/watch?v=7DKFpWnaxLI&ab_channel=HuaHua)