# 2040. Kth Smallest Product of Two Sorted Arrays  

  Methods: Binary Search </br> Difficulty: Hard </br> </br>Given two **sorted 0-indexed **integer arrays nums1 and nums2 as well as an integer k , return *the *kth *(****1-based****) smallest product of *nums1[i] * nums2[j] *where *0 <= i < nums1.length *and*

```plain text
0 <= j < nums2.length
```

.

**Example 1:**

```plain text
Input: nums1 = [2,5], nums2 = [3,4], k = 2
Output: 8
Explanation: The 2 smallest products are:
- nums1[0] * nums2[0] = 2 * 3 = 6
- nums1[0] * nums2[1] = 2 * 4 = 8
The 2nd smallest product is 8.

```

**Example 2:**

```plain text
Input: nums1 = [-4,-2,0,3], nums2 = [2,4], k = 6
Output: 0
Explanation: The 6 smallest products are:
- nums1[0] * nums2[1] = (-4) * 4 = -16
- nums1[0] * nums2[0] = (-4) * 2 = -8
- nums1[1] * nums2[1] = (-2) * 4 = -8
- nums1[1] * nums2[0] = (-2) * 2 = -4
- nums1[2] * nums2[0] = 0 * 2 = 0
- nums1[2] * nums2[1] = 0 * 4 = 0
The 6th smallest product is 0.

```

**Example 3:**

```plain text
Input: nums1 = [-2,-1,0,1,2], nums2 = [-3,-1,2,4,5], k = 3
Output: -6
Explanation: The 3 smallest products are:
- nums1[0] * nums2[4] = (-2) * 5 = -10
- nums1[0] * nums2[3] = (-2) * 4 = -8
- nums1[4] * nums2[0] = 2 * (-3) = -6
The 3rd smallest product is -6.

```

**Constraints:**

- `1 <= nums1.length, nums2.length <= 5 * 104`
- `105 <= nums1[i], nums2[j] <= 105`
- `1 <= k <= nums1.length * nums2.length`
- `nums1` and `nums2` are sorted.
```java
class Solution {
    public long kthSmallestProduct(int[] nums1, int[] nums2, long k) {
        long left = -10000000000L;
        long right = 10000000000L;

        while (left < right) {
            long mid = left + (right - left) / 2;
            if (countProducts(nums1, nums2, mid) < k) 
                left = mid + 1;
            else 
                right = mid;
        }
        return left;
    }

    private long countProducts(int[] nums1, int[] nums2, long target) {
        long count = 0;

        for (int num1 : nums1) {
            if (num1 == 0) {
                if (target >= 0)
                    count += nums2.length;
                continue;
            }

            int low = 0, high = nums2.length;

            while (low < high) {
                int mid = low + (high - low) / 2;
                long product = (long) num1 * nums2[mid];

                if (product <= target) {
                    if (num1 > 0)
                        low = mid + 1;
                    else
                        high = mid;
                } else {
                    if (num1 > 0)
                        high = mid;
                    else
                        low = mid + 1;
                }
            }
            count += (num1 > 0) ? low : nums2.length - low;
        }
        return count;
    }
}
```

