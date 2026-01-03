# 961. N-Repeated Element in Size 2N Array  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given an integer array `nums` with the following properties:

- `nums.length == 2 * n`.
- `nums` contains `n + 1` **unique** elements.
- Exactly one element of `nums` is repeated `n` times.
Return *the element that is repeated *`n`* times*.

**Example 1:**

```plain text
Input: nums = [1,2,3,3]
Output: 3
```

**Example 2:**

```plain text
Input: nums = [2,1,2,5,3,2]
Output: 2
```

**Example 3:**

```plain text
Input: nums = [5,1,5,2,5,3,5,4]
Output: 5
```

**Constraints:**

- `2 <= n <= 5000`
- `nums.length == 2 * n`
- `0 <= nums[i] <= 104`
- `nums` contains `n + 1` **unique** elements and one of them is repeated exactly `n` times.
```java
class Solution {
    public int repeatedNTimes(int[] nums) {
        Arrays.sort(nums);
        int i = 0, cnt = 0;
        for(int num : nums) {
            if(num == i) {
                cnt++;
            } else {
                i = num;
                cnt = 1;
            }
            if(cnt >= nums.length / 2)  
                return i;
        }
        return -1;
    }   
}
```

