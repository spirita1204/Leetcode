# 1498. Number of Subsequences That Satisfy the Given Sum Condition

Methods: Pointer
Difficulty: Medium

**Medium**

2.8K

248

Companies

You are given an array of integers `nums` and an integer `target`.

Return *the number of **non-empty** subsequences of* `nums` *such that the sum of the minimum and maximum element on it is less or equal to* `target`. Since the answer may be too large, return it **modulo** `109 + 7`.

**Example 1:**

```
Input: nums = [3,5,6,7], target = 9
Output: 4
Explanation: There are 4 subsequences that satisfy the condition.
[3] -> Min value + max value <= target (3 + 3 <= 9)
[3,5] -> (3 + 5 <= 9)
[3,5,6] -> (3 + 6 <= 9)
[3,6] -> (3 + 6 <= 9)

```

**Example 2:**

```
Input: nums = [3,3,6,8], target = 10
Output: 6
Explanation: There are 6 subsequences that satisfy the condition. (nums can have repeated numbers).
[3] , [3] , [3,3], [3,6] , [3,6] , [3,3,6]

```

**Example 3:**

```
Input: nums = [2,3,3,4,6,7], target = 12
Output: 61
Explanation: There are 63 non-empty subsequences, two of them do not satisfy the condition ([6,7], [7]).
Number of valid subsequences (63 - 2 = 61).

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 106`
- `1 <= target <= 106`

```java
class Solution {
    public int numSubseq(int[] nums, int target) {
        Arrays.sort(nums);
        int mod = (int)1e9 + 7;
        int count = 0;
        int p1 = 0, p2 = nums.length - 1;

        int[] pows = new int[nums.length];
        pows[0] = 1;

        for (int i = 1 ; i < nums.length ; ++i)// 紀錄2的n次方避免易位
            pows[i] = pows[i - 1] * 2 % mod;

        while(p1<= p2){
            // 只考慮p1 當符合情況代表 選定p1 其[x1,x2,x3..p2]可選可不選的 組合個數
            if(nums[p1] + nums[p2] <= target){
                int pow = p2 - p1;
                count = (count + pows[pow]) % mod;
                p1++;
            }else {
                p2--;
            }
        }    
        return count;
    }
}
```