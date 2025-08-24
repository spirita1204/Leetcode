# 1493. Longest Subarray of 1's After Deleting One Element  

  Methods: Pointer </br> Difficulty: Medium </br> </br>Given a binary array `nums`, you should delete one element from it.

Return *the size of the longest non-empty subarray containing only *`1`*'s in the resulting array*. Return `0` if there is no such subarray.

**Example 1:**

```plain text
Input: nums = [1,1,0,1]
Output: 3
Explanation: After deleting the number in position 2, [1,1,1] contains 3 numbers with value of 1's.
```

**Example 2:**

```plain text
Input: nums = [0,1,1,1,0,1,1,0,1]
Output: 5
Explanation: After deleting the number in position 4, [0,1,1,1,1,1,0,1] longest subarray with value of 1's is [1,1,1,1,1].
```

**Example 3:**

```plain text
Input: nums = [1,1,1]
Output: 2
Explanation: You must delete one element.
```

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.
```java
class Solution {
    public int longestSubarray(int[] nums) {
        int start = 0;
        int end = 0;
        int zeros = 0;

        while(end < nums.length) {
            if (nums[end] == 0) {
                zeros++;
            }
            end++;
            if (zeros > 1) {
                if (nums[start] == 0) {
                    zeros--;
                }
                start++;
            }
        }
        return end - start - 1;
    }
}
```

