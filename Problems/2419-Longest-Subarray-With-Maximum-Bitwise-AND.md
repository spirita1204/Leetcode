# 2419. Longest Subarray With Maximum Bitwise AND  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

Hint

You are given an integer array `nums` of size `n`.

Consider a **non-empty** subarray from `nums` that has the **maximum** possible **bitwise AND**.

- In other words, let `k` be the maximum value of the bitwise AND of **any** subarray of `nums`. Then, only subarrays with a bitwise AND equal to `k` should be considered.
Return *the length of the ****longest**** such subarray*.

The bitwise AND of an array is the bitwise AND of all the numbers in it.

A **subarray** is a contiguous sequence of elements within an array.

**Example 1:**

```plain text
Input: nums = [1,2,3,3,2,2]
Output: 2
Explanation:
The maximum possible bitwise AND of a subarray is 3.
The longest subarray with that value is [3,3], so we return 2.

```

**Example 2:**

```plain text
Input: nums = [1,2,3,4]
Output: 1
Explanation:
The maximum possible bitwise AND of a subarray is 4.
The longest subarray with that value is [4], so we return 1.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 106`
```java
class Solution {
    public int longestSubarray(int[] nums) {
        // the bitwise AND of two different numbers will always be strictly less than the maximum of those two numbers.
        // 等於找最大連續數字長度
        int max = 0;// 最大值
        int cnt = 0;// 當前最大
        int maxValMaxLen = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] > max) {
                cnt = 0;
                max = nums[i];
                maxValMaxLen = 1;
            } 
            if(nums[i] < max) {
                maxValMaxLen = Math.max(maxValMaxLen, cnt);
                cnt = 0;
            }
            if(max == nums[i]) 
                cnt++;
            // 計算全局最大
        }
        maxValMaxLen = Math.max(maxValMaxLen, cnt);
        return maxValMaxLen;
    }   
}
```

