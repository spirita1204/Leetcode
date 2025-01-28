# 713. Subarray Product Less Than K

Methods: Pointer
Difficulty: Medium

**Medium**

5.3K

168

Companies

Given an array of integers `nums` and an integer `k`, return *the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than* `k`.

**Example 1:**

```
Input: nums = [10,5,2,6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

```

**Example 2:**

```
Input: nums = [1,2,3], k = 0
Output: 0

```

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `1 <= nums[i] <= 1000`
- `0 <= k <= 106`

```jsx
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        //sliding window //time compl : O(n)
        if (k <= 1) return 0;// 乘積都會大於等於1
        int count = 0;
        int left = 0;
        int right = 0;
        int prod = 1;//相乘結果

        while(right < nums.length){
            prod *= nums[right];
        
            while (prod >= k) {
                prod /= nums[left];
                left++;
            }
            count += (right - left + 1);// 新增符合條件的 
            right++;
        }
        return count;
    }
}
```