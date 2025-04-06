# 368. Largest Divisible Subset  

  Methods: DP </br> Difficulty: Medium </br> </br>***NOTE:- if you found anyone's post helpful please upvote that post because some persons are downvoting unneccesarily, and you are the one guys that save our post from getting unvisible, upvote for remains visible for others so and other people can also get benefitted***

**DESCRIPTION:-**

**Given an array the task is to largest divisible subset in array. A subset is called divisible if for every pair (x, y) in subset, either x divides y or y divides x.**

**Examples:**

Input : arr[] = {1, 16, 7, 8, 4}Output : 16 8 4 1 or 1 4 8 16

**An efficient solution involves following steps.**

- *1. Sort all array elements in increasing order. The purpose of sorting is to make sure that all divisors of an element appear before it.2. Create an array dp[] of same size as input array. dp[i] stores size of divisible subset ending with arr[i] (In sorted array). The minimum value of dp[i] would be 1.
1. Traverse all array elements. For every element, find a divisor arr[j] with largest value of dp[j] and store the value of dp[i] as dp[j] + 1.**
![Image](https://assets.leetcode.com/users/amit_gupta10/image_1592042710.png)

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;

        int prev[] = new int[n];// 紀錄上個可整除值位置 串起來(輸出用)
        int dp[] = new int[n];// 使用前i元素可以組成之最長Divisible Subset
        int max = 0;
        int index = 0;
        dp[0] = 0;

        for (int i = 0; i < n; i++) {
            prev[i] = -1;
            for (int j = i - 1; j >= 0; j--) {
                if (nums[i] % nums[j] == 0 && dp[j] + 1 > dp[i]) {// 指到上一個 不要繼續往下指 
                    prev[i] = j;
                    dp[i] = dp[j] + 1;// 紀錄長度
                }
            }
            if (dp[i] > max) {// sub最多
                max = dp[i];
                index = i;// point 指到最多
            }
        }
        List<Integer> res = new ArrayList<>();
        while (index > -1) {
            res.add(nums[index]);
            index = prev[index];
        }
        return res;
    }
}
```

