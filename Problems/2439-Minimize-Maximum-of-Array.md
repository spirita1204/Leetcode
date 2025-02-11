# 2439. Minimize Maximum of Array

Methods: Binary Search
Difficulty: Medium

**Medium**

1K

255

Companies

You are given a **0-indexed** array `nums` comprising of `n` non-negative integers.

In one operation, you must:

- Choose an integer `i` such that `1 <= i < n` and `nums[i] > 0`.
- Decrease `nums[i]` by 1.
- Increase `nums[i - 1]` by 1.

Return *the **minimum** possible value of the **maximum** integer of* `nums` *after performing **any** number of operations*.

**Example 1:**

```
Input: nums = [3,7,1,6]
Output: 5
Explanation:
One set of optimal operations is as follows:
1. Choose i = 1, and nums becomes [4,6,1,6].
2. Choose i = 3, and nums becomes [4,6,2,5].
3. Choose i = 1, and nums becomes [5,5,2,5].
The maximum integer of nums is 5. It can be shown that the maximum number cannot be less than 5.
Therefore, we return 5.

```

**Example 2:**

```
Input: nums = [10,1]
Output: 10
Explanation:
It is optimal to leave nums as is, and since 10 is the maximum value, we return 10.

```

**Constraints:**

- `n == nums.length`
- `2 <= n <= 105`
- `0 <= nums[i] <= 109`

```java
class Solution {
    public int minimizeArrayValue(int[] nums) {
        //從最後一位開始處理 遞補
        int left = 0;
        int right = (int) 1e9+7;

        while(left <= right){
            int mid = left + (right- left)/ 2;
            long extra = 0;//避免易位
            for(int i = nums.length - 1; i>= 0; i--){
                long total = nums[i] + extra;//避免易位
                if(total <= mid){
                    extra = 0;
                }else if(total > mid){
                    extra = total - mid;
                }
            }
            if(extra > 0){
                left = mid + 1;
            }else if(extra == 0){
                right = mid - 1;
            }
        }
        return left;
    }
}
```