# 2342. Max Sum of a Pair With Equal Sum of Digits  

  Methods: Array </br> Data Structure: Heap </br> Difficulty: Medium </br> </br>You are given a **0-indexed** array `nums` consisting of **positive** integers. You can choose two indices `i` and `j`, such that `i != j`, and the sum of digits of the number `nums[i]` is equal to that of `nums[j]`. 

Return *the ****maximum**** value of *`nums[i] + nums[j]`* that you can obtain over all possible indices *`i`* and *`j`* that satisfy the conditions.*

**Example 1:**

```plain text
Input: nums = [18,43,36,13,7]
Output: 54
Explanation: The pairs (i, j) that satisfy the conditions are:
- (0, 2), both numbers have a sum of digits equal to 9, and their sum is 18 + 36 = 54.
- (1, 4), both numbers have a sum of digits equal to 7, and their sum is 43 + 7 = 50.
So the maximum sum that we can obtain is 54.

```

**Example 2:**

```plain text
Input: nums = [10,12,19,14]
Output: -1
Explanation: There are no two numbers that satisfy the conditions, so we return -1.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
Hint 1

What is the largest possible sum of digits a number can have?

---

Hint 2

Group the array elements by the sum of their digits, and find the largest two elements of each group.

```java
class Solution {
    public int maximumSum(int[] nums) {
        // 依據
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> 
            sumOfDigits(a) == sumOfDigits(b) ? b - a : sumOfDigits(a) - sumOfDigits(b)
        );
        for(int num : nums) {
            pq.offer(num);
        }
        int max = 0;
        while(!pq.isEmpty()) {
            int e = pq.poll();
            if(!pq.isEmpty()) 
                if(sumOfDigits(pq.peek()) == sumOfDigits(e)) {
                    int e2 = pq.poll();
                    max = Math.max(e + e2, max);
                    while(!pq.isEmpty() && sumOfDigits(pq.peek()) == sumOfDigits(e2))
                        pq.poll();
                }
        }
        return max == 0? -1: max;
    }
    private int sumOfDigits (int num) {
        int sum = 0;
        while(num > 0) {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }
}
```

最優解

```java
class Solution {
    public int maximumSum(int[] nums) {
        int[] max = new int[100];
        int ans = -1;
        for (int x : nums) {
            int dsum = 0;
            int temp = x;
            dsum = sumOfDigits(temp);
            if (max[dsum] != 0)
                ans = Math.max(ans, x + max[dsum]);
            max[dsum] = Math.max(max[dsum], x);
        }
        return ans;
    }

    private int sumOfDigits(int num) {
        int sum = 0;
        while (num > 0) {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }
}
```

