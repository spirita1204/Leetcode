# 3101. Count Alternating Subarrays

Methods: Pointer
Difficulty: Medium

You are given a binary array nums.

We call a subarray **alternating** if **no** two **adjacent** elements in the subarray have the **same** value.

Return *the number of alternating subarrays in* `nums`.

**Example 1:**

```java
**Input:** nums = [0,1,1,1]

**Output:** 5

**Explanation:**

The following subarrays are alternating: `[0]`, `[1]`, `[1]`, `[1]`, and `[0,1]`.
```

**Example 2:**

```java
**Input:** nums = [1,0,1,0]

**Output:** 10

**Explanation:**

Every subarray of the array is alternating. There are 10 possible subarrays that we can choose.
```

**Constraints:**

- `1 <= nums.length <= 105`
- `nums[i]` is either `0` or `1`.

```java
class Solution {
    public long countAlternatingSubarrays(int[] nums) {
        // Compare the current element with the previous element.
        // If they are different, increase the length of the window.
        // If they are same, then calculate the number of subarrays that can be created.
        int p1 = 0, p2 = 1;
        long sum = 0;
        long length = 0;

        while(p2 < nums.length) {
            if(nums[p2 - 1] != nums[p2]) {
                p2++;
            } else {
                length = p2 - p1;
                sum += (length)* (length + 1) / 2;
                p1 = p2;
                p2++;
            }
        }
        // 最後到終點round
        length = p2 - p1;
        sum += (length)* (length + 1) / 2;
        
        return sum;
    }
}
```