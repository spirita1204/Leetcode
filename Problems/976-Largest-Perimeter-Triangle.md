# 976. Largest Perimeter Triangle

Methods: Basic logic
Difficulty: Easy

**Easy**

2.7K

383

Companies

Given an integer array `nums`, return *the largest perimeter of a triangle with a non-zero area, formed from three of these lengths*. If it is impossible to form any triangle of a non-zero area, return `0`.

**Example 1:**

```
Input: nums = [2,1,2]
Output: 5
Explanation: You can form a triangle with three side lengths: 1, 2, and 2.

```

**Example 2:**

```
Input: nums = [1,2,1,10]
Output: 0
Explanation:
You cannot use the side lengths 1, 1, and 2 to form a triangle.
You cannot use the side lengths 1, 1, and 10 to form a triangle.
You cannot use the side lengths 1, 2, and 10 to form a triangle.
As we cannot use any three side lengths to form a triangle of non-zero area, we return 0.

```

**Constraints:**

- `3 <= nums.length <= 104`
- `1 <= nums[i] <= 106`

```java
class Solution {
    public int largestPerimeter(int[] nums) {
        //a + b > c
        Arrays.sort(nums);
        int p = nums.length - 1;
        while(p-2 >= 0){
            if(nums[p] >= nums[p - 1] + nums[p - 2]) p--;
            else break;
        } 
        return (p-2 < 0) ? 0 : nums[p-2] + nums[p-1] + nums[p];
    }
}
```