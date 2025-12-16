# 962. Maximum Width Ramp  

  Methods: Pointer </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

A **ramp** in an integer array `nums` is a pair `(i, j)` for which `i < j` and `nums[i] <= nums[j]`. The **width** of such a ramp is `j - i`.

Given an integer array `nums`, return *the maximum width of a ****ramp**** in *`nums`. If there is no **ramp** in `nums`, return `0`.

**Example 1:**

```plain text
Input: nums = [6,0,8,2,1,5]
Output: 4
Explanation: The maximum width ramp is achieved at (i, j) = (1, 5): nums[1] = 0 and nums[5] = 5.

```

**Example 2:**

```plain text
Input: nums = [9,8,1,0,1,9,4,0,4,1]
Output: 7
Explanation: The maximum width ramp is achieved at (i, j) = (2, 9): nums[2] = 1 and nums[9] = 1.

```

**Constraints:**

- `2 <= nums.length <= 5 * 104`
- `0 <= nums[i] <= 5 * 104`
```java
class Solution {
    public int maxWidthRamp(int[] nums) {
        int n = nums.length;
        int[] rightMax = new int[n];
        rightMax[n - 1] = nums[n - 1];
        for(int i = n - 2; i >= 0; i--) 
            rightMax[i] = Math.max(nums[i], rightMax[i + 1]);
        int left = 0, right = 0;
        int maxWidth = 0;
        while(right < n) {
            while (left < right && nums[left] > rightMax[right]) {
                left++;
            }
            maxWidth = Math.max(maxWidth, right - left);
            right++;
        }
        return maxWidth;
    }
}
```

