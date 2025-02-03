# 3105. Longest Strictly Increasing or Strictly Decreasing Subarray  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given an array of integers `nums`. Return *the length of the ****longest*****

*subarray*

*of*

```plain text
nums
```

*which is either ****strictly increasing**** or ****strictly decreasing***

.

**Example 1:**

**Input:** nums = [1,4,3,3,2]

**Output:** 2

**Explanation:**

The strictly increasing subarrays of `nums` are `[1]`, `[2]`, `[3]`, `[3]`, `[4]`, and `[1,4]`.

The strictly decreasing subarrays of `nums` are `[1]`, `[2]`, `[3]`, `[3]`, `[4]`, `[3,2]`, and `[4,3]`.

Hence, we return `2`.

**Example 2:**

**Input:** nums = [3,3,3,3]

**Output:** 1

**Explanation:**

The strictly increasing subarrays of `nums` are `[3]`, `[3]`, `[3]`, and `[3]`.

The strictly decreasing subarrays of `nums` are `[3]`, `[3]`, `[3]`, and `[3]`.

Hence, we return `1`.

**Example 3:**

**Input:** nums = [3,2,1]

**Output:** 3

**Explanation:**

The strictly increasing subarrays of `nums` are `[3]`, `[2]`, and `[1]`.

The strictly decreasing subarrays of `nums` are `[3]`, `[2]`, `[1]`, `[3,2]`, `[2,1]`, and `[3,2,1]`.

Hence, we return `3`.

**Constraints:**

- `1 <= nums.length <= 50`
- `1 <= nums[i] <= 50`
```java
class Solution {
    public int longestMonotonicSubarray(int[] nums) {
        int p1 = 0, p2 = 0;// 指標
        int lis = 0, lds = 0;// 最長increase decrease

        while(p2 < nums.length) {
            if((p1 == 0 && p2 == 0) || nums[p2] > nums[p2 - 1])
                p2++;
            else {
                lis = Math.max(lis, p2 - p1);
                p1 = p2;
                p2++;
            }
        }
        if(p2 == nums.length)
            lis = Math.max(lis, p2 - p1);
            
        p1 = nums.length - 1;
        p2 = nums.length - 1;

        while(p2 >= 0) {
            if((p1 == nums.length - 1 && p2 == nums.length - 1) || nums[p2 + 1] < nums[p2])
                p2--;
            else {
                lds = Math.max(lds, p1 - p2);
                p1 = p2;
                p2--;
            }
        }
        if(p2 == -1)
            lds = Math.max(lds, p1 - p2);
        return Math.max(lis, lds);
    }
}
```

