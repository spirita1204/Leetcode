# 2425. Bitwise XOR of All Pairings  

  Methods: Bitwise </br> Difficulty: Medium </br> </br>You are given two **0-indexed** arrays, `nums1` and `nums2`, consisting of non-negative integers. There exists another array, `nums3`, which contains the bitwise XOR of **all pairings** of integers between `nums1` and `nums2` (every integer in `nums1` is paired with every integer in `nums2` **exactly once**).

Return* the ****bitwise XOR**** of all integers in *`nums3`.

**Example 1:**

```plain text
Input: nums1 = [2,1,3], nums2 = [10,2,5,0]
Output: 13
Explanation:
A possible nums3 array is [8,0,7,2,11,3,4,1,9,1,6,3].
The bitwise XOR of all these numbers is 13, so we return 13.

```

**Example 2:**

```plain text
Input: nums1 = [1,2], nums2 = [3,4]
Output: 0
Explanation:
All possible pairs of bitwise XORs are nums1[0] ^ nums2[0], nums1[0] ^ nums2[1], nums1[1] ^ nums2[0],
and nums1[1] ^ nums2[1].
Thus, one possible nums3 array is [2,5,1,6].
2 ^ 5 ^ 1 ^ 6 = 0, so we return 0.

```

**Constraints:**

- `1 <= nums1.length, nums2.length <= 105`
- `0 <= nums1[i], nums2[j] <= 109`
```java
class Solution {
    public int xorAllNums(int[] nums1, int[] nums2) {
        // 2 10
        // 2 2
        // 2 5 
        // 2 0
        // 1 10 
        // 1 2 
        // 1 5
        // 1 0
        // 3 10
        // 3 2
        // 3 5
        // 3 0
        // 1010
        // 0010
        // 0101
        // 0000 -> 1101
        int len1 = nums1.length, len2 = nums2.length;
        int res1 = 0, res2 = 0;
        if(len1 % 2 == 0 && len2 % 2 == 0)
            return 0;
        
        for(int num: nums1)
            res1 ^= num;
        for(int num: nums2)
            res2 ^= num;
        if(len1 % 2 == 0) 
            return res1;
        if(len2 % 2 == 0) 
            return res2;
        else 
            return res1 ^ res2;
    }
}
```

