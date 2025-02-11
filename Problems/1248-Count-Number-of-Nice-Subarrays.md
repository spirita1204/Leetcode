# 1248. Count Number of Nice Subarrays

Methods: Prefix Sum
Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Hint

Given an array of integers `nums` and an integer `k`. A continuous subarray is called **nice** if there are `k` odd numbers on it.

Return *the number of **nice** sub-arrays*.

**Example 1:**

```
Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].

```

**Example 2:**

```
Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There are no odd numbers in the array.

```

**Example 3:**

```
Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16

```

**Constraints:**

- `1 <= nums.length <= 50000`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= nums.length`

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        Map<Integer, Integer> hm = new HashMap<>();
        hm.put(0, 1);// 初始值
        int res = 0;

        for(int i = 0; i < nums.length; i++) {
            if(i == 0) {
                nums[0] = (nums[0] % 2 == 0) ? 0: 1;
            } else {
                if(nums[i] % 2 == 0) nums[i] = nums[i - 1];
                else nums[i] = nums[i - 1] + 1;
            }
            // 數字 -> 出現幾次
            hm.put(nums[i], hm.getOrDefault(nums[i], 0) + 1);
            // 找出剛好等於nums[i] - k 代表剛好存在k個 奇數
            if(hm.containsKey(nums[i] - k)) res += hm.get(nums[i] - k);
        }
        return res;
    }
}
```