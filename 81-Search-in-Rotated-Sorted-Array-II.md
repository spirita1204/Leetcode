# 81. Search in Rotated Sorted Array II

Methods: Binary Search
Difficulty: Medium

Medium

Topics

Companies

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true` *if* `target` *is in* `nums`*, or* `false` *if it is not in* `nums`*.*

You must decrease the overall operation steps as much as possible.

**Example 1:**

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true

```

**Example 2:**

```
Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false

```

**Constraints:**

- `1 <= nums.length <= 5000`
- `104 <= nums[i] <= 104`
- `nums` is guaranteed to be rotated at some pivot.
- `104 <= target <= 104`

**Follow up:** This problem is similar to [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/), but `nums` may contain **duplicates**. Would this affect the runtime complexity? How and why?

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        // 將[1,0,1,1,1]後面干擾的 1同首位刪掉 (nums[mid] >= nums[0]) == (target >= nums[0])就會成立
        int len = nums.length;
        while(len-- > 1 && nums[0] == nums[r]) r --;

        // 重點: 判斷nums[mid]和target是否在同個區間->跟nums[0]做判斷
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target)
                return true;
            if ((nums[mid] >= nums[0]) == (target >= nums[0])) {// 代表在同一區間
                // 照傳統
                if (nums[mid] < target) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
            // 其他情況直接判斷在哪區間
            else if (target >= nums[0]) {//
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return false;
    }
}
```