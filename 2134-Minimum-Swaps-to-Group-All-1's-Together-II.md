# 2134. Minimum Swaps to Group All 1's Together II

Methods: Pointer
Difficulty: Medium

Medium

Topics

Companies

Hint

A **swap** is defined as taking two **distinct** positions in an array and swapping the values in them.

A **circular** array is defined as an array where we consider the **first** element and the **last** element to be **adjacent**.

Given a **binary** **circular** array `nums`, return *the minimum number of swaps required to group all* `1`*'s present in the array together at **any location***.

**Example 1:**

```
Input: nums = [0,1,0,1,1,0,0]
Output: 1
Explanation: Here are a few of the ways to group all the 1's together:
[0,0,1,1,1,0,0] using 1 swap.
[0,1,1,1,0,0,0] using 1 swap.
[1,1,0,0,0,0,1] using 2 swaps (using the circular property of the array).
There is no way to group all 1's together with 0 swaps.
Thus, the minimum number of swaps required is 1.

```

**Example 2:**

```
Input: nums = [0,1,1,1,0,0,1,1,0]
Output: 2
Explanation: Here are a few of the ways to group all the 1's together:
[1,1,1,0,0,0,0,1,1] using 2 swaps (using the circular property of the array).
[1,1,1,1,1,0,0,0,0] using 2 swaps.
There is no way to group all 1's together with 0 or 1 swaps.
Thus, the minimum number of swaps required is 2.

```

**Example 3:**

```
Input: nums = [1,1,0,0,1]
Output: 0
Explanation: All the 1's are already grouped together due to the circular property of the array.
Thus, the minimum number of swaps required is 0.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.

```java
class Solution {
    public int minSwaps(int[] nums) {
        int len = nums.length;
        // 複製原陣列到原本後面
        int[] nums2 = new int[len * 2];
        // 有多少個1
        int ones = 0;
        for(int i = 0; i < len* 2; i++) {
            nums2[i] = nums[i % len];
            if(nums[i % len] == 1) ones++;
        }
        ones /= 2;// 當作slide window的wnidow size用
        int onesInWindow = 0;
        int p1 = 0;// 前指標
        int max = 0;// window中最多有幾個1
        for(int i = 0; i < len* 2; i++) {
            if(i - p1 >= ones) {// 大於window
                if(nums2[p1] == 1) onesInWindow--;
                p1++;
            } 
            if(nums2[i] == 1) onesInWindow++;
            max = Math.max(max, onesInWindow);
        }
        return ones - max;
    }
}
```