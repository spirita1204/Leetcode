# 209. Minimum Size Subarray Sum

Methods: Binary Search
Difficulty: Medium

**Medium**

9.2K

253

Companies

Given an array of positive integers `nums` and a positive integer `target`, return *the **minimal length** of a*

*subarray*

*whose sum is greater than or equal to*

```
target
```

. If there is no such subarray, return

```
0
```

instead.

**Example 1:**

```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

```

**Example 2:**

```
Input: target = 4, nums = [1,4,4]
Output: 1

```

**Example 3:**

```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0

```

**Constraints:**

- `1 <= target <= 109`
- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 104`

**Follow up:**

If you have figured out the

```
O(n)
```

solution, try coding another solution of which the time complexity is

```
O(n log(n))
```

.

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int[] sums = new int[nums.length + 1];
        int min = Integer.MAX_VALUE;
        for (int i = 1; i < sums.length; i++) sums[i] = sums[i - 1] + nums[i - 1];// skill
        //sums[] = {0 2 5 6 8 12 15}
        for (int i = 0; i < sums.length; i++) {// i為起始點 並透過bs往後找剛好可以>=target的節點
            int left = i + 1;
            int right = sums.length - 1;
            int key = target + sums[i];// 

            while(left <= right){
                int mid = left + (right - left)/2;
                if(sums[mid] >= key) right = mid -1;
                else left = mid + 1;
            }
            if(left == sums.length) break;// 加總還不夠
            min = Math.min(min, left - i);
        }
        return (min == Integer.MAX_VALUE) ? 0 : min;    
    }
}
```