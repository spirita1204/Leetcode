# 34. Find First and Last Position of Element in Sorted Array

Methods: Binary Search
Difficulty: Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

```

**Example 3:**

```
Input: nums = [], target = 0
Output: [-1,-1]

```

**Constraints:**

- `0 <= nums.length <= 105`
- `109 <= nums[i] <= 109`
- `nums` is a non-decreasing array.
- `109 <= target <= 109`

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {//binary search
        if(nums.length == 0) return new int[]{-1, -1};
        int left = 0, right = nums.length-1;
        int[] res = new int[2];
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] < target){
                left = mid + 1;
            }else if(nums[mid] >= target){
                right = mid - 1;
            }
        }
        if(left > nums.length-1 || left < 0 || nums[left] != target) return new int[]{-1, -1};
        res[0] = left;
        right = nums.length-1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] <= target){
                left = mid + 1;
            }else if(nums[mid] > target){
                right = mid - 1;
            }
        }
        res[1] = right;
        return res;
    }
}
```