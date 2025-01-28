# 2364. Count Number of Bad Pairs

Data structure: Hash Table
Difficulty: Medium
Similar: 1814

Medium

Topics

Companies

Hint

You are given a **0-indexed** integer array `nums`. A pair of indices `(i, j)` is a **bad pair** if `i < j` and `j - i != nums[j] - nums[i]`.

Return *the total number of **bad pairs** in* `nums`.

**Example 1:**

```
Input: nums = [4,1,3,3]
Output: 5
Explanation: The pair (0, 1) is a bad pair since 1 - 0 != 1 - 4.
The pair (0, 2) is a bad pair since 2 - 0 != 3 - 4, 2 != -1.
The pair (0, 3) is a bad pair since 3 - 0 != 3 - 4, 3 != -1.
The pair (1, 2) is a bad pair since 2 - 1 != 3 - 1, 1 != 2.
The pair (2, 3) is a bad pair since 3 - 2 != 3 - 3, 1 != 0.
There are a total of 5 bad pairs, so we return 5.

```

**Example 2:**

```
Input: nums = [1,2,3,4,5]
Output: 0
Explanation: There are no bad pairs.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`

## **Time Limit Exceeded**

```java
class Solution {
    public long countBadPairs(int[] nums) {
        long res = 0;
        // j - i != nums[j] - nums[i].等同於
        // nums[i] - i != nums[j] - j  
        for(int i = 0; i < nums.length; i++) {
            nums[i] -= i;// 4 0 1 0 =>>  4->1, 0->2, 1->1
        }
        for(int i = 0; i < nums.length; i++) {
            for(int j = i + 1; j < nums.length; j++) {
                if(nums[i] != nums[j])
                    res++;
            } 
        }
        return res;
    }
}
```

## **Accepted**

```java
class Solution {
    public long countBadPairs(int[] nums) {
        long res = 0;
        Map<Integer, Integer> hm = new HashMap<>();
        // j - i != nums[j] - nums[i].等同於
        // nums[i] - i != nums[j] - j
        for (int i = 0; i < nums.length; i++) {
            // 4 0 1 0 =>>  4->1, 0->2, 1->1
            int prev = hm.getOrDefault(nums[i] - i, 0);
            res += i - prev;// Invalid = Total - Valid
            hm.put(nums[i] - i, prev + 1);
        }
        return res;
    }
}
```