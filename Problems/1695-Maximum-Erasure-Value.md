# 1695. Maximum Erasure Value  

  Methods: Sliding Window </br> Difficulty: Medium </br> </br>You are given an array of positive integers `nums` and want to erase a subarray containing **unique elements**. The **score** you get by erasing the subarray is equal to the **sum** of its elements.

Return *the ****maximum score**** you can get by erasing ****exactly one**** subarray.*

An array `b` is called to be a subarray of `a` if it forms a contiguous subsequence of `a`, that is, if it is equal to `a[l],a[l+1],...,a[r]` for some `(l,r)`.

**Example 1:**

```plain text
Input: nums = [4,2,4,5,6]
Output: 17
Explanation: The optimal subarray here is [2,4,5,6].
```

**Example 2:**

```plain text
Input: nums = [5,2,1,2,5,2,1,2,5]
Output: 8
Explanation: The optimal subarray here is [5,2,1] or [1,2,5].
```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 104`
```java
class Solution {
    public int maximumUniqueSubarray(int[] nums) {
        // slide window
        int p1 = 0, p2 = 0;
        int len = nums.length;
        Set<Integer> hm = new HashSet<>();
        int sum = 0, res = 0;

        while(p2 < len) {
            while(hm.contains(nums[p2])) {
                sum -= nums[p1];
                hm.remove(nums[p1]);
                p1++;
            }
            sum += nums[p2];
            hm.add(nums[p2]);
            res = Math.max(res, sum);
            p2++;
        }
        return res;
    }
}
```

