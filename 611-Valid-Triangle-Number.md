# 611. Valid Triangle Number

Methods: Binary Search
Difficulty: Medium

Medium

Topics

Companies

Given an integer array `nums`, return *the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle*.

**Example 1:**

```
Input: nums = [2,2,3,4]
Output: 3
Explanation: Valid combinations are:
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3

```

**Example 2:**

```
Input: nums = [4,2,3,4]
Output: 4

```

**Constraints:**

- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 1000`

```java
class Solution {
    public int triangleNumber(int[] nums) {
        Arrays.sort(nums);// 只要比較c> a+ b
        int count = 0;
        
        for(int i= 0; i< nums.length; i++) {
            for(int j = i + 1; j< nums.length; j++) {
                // 取出a, b 並相加 去找c> a+ b
                int target = nums[i] + nums[j];
                count += countGreaterOrEqualMid(nums, target, j);
            }
        }
        return count;
    }
    private int countGreaterOrEqualMid(int[] nums, int target, int j) {
        int left = 0;
        int right = nums.length - 1;
        
        while(left <= right) {
            int mid = left + (right - left) / 2;
            if(target > nums[mid]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return ((left - 1) - j <= 0)? 0: (left - 1) - j;// 將剛好大於 減掉 b 中間範圍都可以取
    }
}
```