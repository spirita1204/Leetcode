# 3191. Minimum Operations to Make Binary Array Elements Equal to One I  

  Methods: Greedy </br> Difficulty: Medium </br> </br>You are given a binary array `nums`.

You can do the following operation on the array **any** number of times (possibly zero):

- Choose **any** 3 **consecutive** elements from the array and **flip** **all** of them.
**Flipping** an element means changing its value from 0 to 1, and from 1 to 0.

Return the **minimum** number of operations required to make all elements in `nums` equal to 1. If it is impossible, return -1.

**Example 1:**

**Input:** nums = [0,1,1,1,0,0]

**Output:** 3

**Explanation:**

We can do the following operations:

- Choose the elements at indices 0, 1 and 2. The resulting array is `nums = [``<u>**1**</u>``,``<u>**0**</u>``,``<u>**0**</u>``,1,0,0]`.
- Choose the elements at indices 1, 2 and 3. The resulting array is `nums = [1,``<u>**1**</u>``,``<u>**1**</u>``,``<u>**0**</u>``,0,0]`.
- Choose the elements at indices 3, 4 and 5. The resulting array is `nums = [1,1,1,``<u>**1**</u>``,``<u>**1**</u>``,``<u>**1**</u>``]`.
**Example 2:**

**Input:** nums = [0,1,1,1]

**Output:** -1

**Explanation:**

It is impossible to make all elements equal to 1.

**Constraints:**

- `3 <= nums.length <= 105`
- `0 <= nums[i] <= 1`  
```java
class Solution {
    public int minOperations(int[] nums) {
        // greedy 從最左邊開始思考
        int p1 = 0;
        int cnt = 0;

        while(p1 < nums.length) {
            if(nums[p1] == 0) {
                if(p1 + 2 < nums.length) {
                    nums[p1] = 1;
                    nums[p1 + 1] = nums[p1 + 1] == 1? 0: 1;
                    nums[p1 + 2] = nums[p1 + 2] == 1? 0: 1;
                    cnt++;
                } else 
                    return -1;
            } else 
                p1++;
        }
        return cnt;
    }
}
```

