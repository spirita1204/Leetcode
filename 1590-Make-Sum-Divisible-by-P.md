# 1590. Make Sum Divisible by P

Methods: Prefix Sum
Difficulty: Medium++

Medium

Topics

Companies

Hint

Given an array of positive integers `nums`, remove the **smallest** subarray (possibly **empty**) such that the **sum** of the remaining elements is divisible by `p`. It is **not** allowed to remove the whole array.

Return *the length of the smallest subarray that you need to remove, or* `-1` *if it's impossible*.

A **subarray** is defined as a contiguous block of elements in the array.

**Example 1:**

```
Input: nums = [3,1,4,2], p = 6
Output: 1
Explanation: The sum of the elements in nums is 10, which is not divisible by 6. We can remove the subarray [4], and the sum of the remaining elements is 6, which is divisible by 6.

```

**Example 2:**

```
Input: nums = [6,3,5,2], p = 9
Output: 2
Explanation: We cannot remove a single element to get a sum divisible by 9. The best way is to remove the subarray [5,2], leaving us with [6,3] with sum 9.

```

**Example 3:**

```
Input: nums = [1,2,3], p = 3
Output: 0
Explanation: Here the sum is 6. which is already divisible by 3. Thus we do not need to remove anything.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
- `1 <= p <= 109`

```java
class Solution {
    public int minSubarray(int[] nums, int p) {
        long sum = 0;
        int len = nums.length;
        Map<Integer, Integer> hm = new HashMap<>();
        for(int e: nums)// 先求總額
            sum += e;
        if(sum % p == 0) return 0;// 當下即滿足
        if(sum < p) return -1;
        long r = sum % p; // 总和对p的余数
        // 如果总和已经可以被p整除，则不需要移除任何子数组
        if (r == 0) return 0;
        long pSum = 0;
        int minSubLen = len;
        hm.put(0, -1); // 初始化，处理从开头移除子数组的情况
        for(int i = 0; i < len; i++) {
            pSum += nums[i];
            int currentMod = (int)(pSum % p);
            int targetMod = (int)(currentMod - r + p) % p; // 确保非负
            // 查找是否有可以抵消的余数，使得我们可以删除某个子数组
            if(hm.containsKey(targetMod)) {
                minSubLen = Math.min(minSubLen, i - hm.get(targetMod));
            }
            hm.put(currentMod, i); 
        }
        return (len == minSubLen)? -1: minSubLen;// 不可能
    }
}
```