# 907. Sum of Subarray Minimums

Data structure: Stack
Difficulty: Medium

Medium

Topics

Companies

Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `109 + 7`.

**Example 1:**

```
Input: arr = [3,1,2,4]
Output: 17
Explanation:
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4].
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.

```

**Example 2:**

```
Input: arr = [11,81,94,43,3]
Output: 444

```

**Constraints:**

- `1 <= arr.length <= 3 * 104`
- `1 <= arr[i] <= 3 * 104`

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {// 需考慮 重複[71,55,82,55] 左右界會有問題
        // x 0 [3 2 4 5] 1 x x                               ^     ^
        //        ^
        // 左邊界 右邊界 2 * 3 種
        //         ret += 2 * 6
        //             += 4 * ?
        //             += 5 * ?
        int n = arr.length;
        double m = 1e9 + 7;
        int sum = 0;
        int[] preSmaller = new int[n];
        int[] nextSmaller = new int[n];
        Arrays.fill(preSmaller, -1);
        Arrays.fill(nextSmaller, -1);
        Stack<Integer> st = new Stack<>();
        Stack<Integer> st2 = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {// 左
            while (!st.isEmpty() && arr[st.peek()] >= arr[i]) {// skill 判斷>= 讓重複數字 直接對應到上一個 出現位置
                preSmaller[st.pop()] = i;
            }
            st.push(i);
        }   
        for (int i = 0; i < n; i++) {// 右界
            while (!st2.isEmpty() && arr[st2.peek()] > arr[i]) {
                nextSmaller[st2.pop()] = i;
            }
            st2.push(i);
        }   
        for(int i = 0; i < n; i++) {
            long count = arr[i];
            if(nextSmaller[i] == -1) {
                count *= n - i;
            } else {
                count *= (nextSmaller[i] - i);
            } 
            if(preSmaller[i] == -1) {
                count *= i - 0 + 1;
            } else {
                count *= (i - preSmaller[i]);
            }
            count %= m;
            sum += count;
            sum %=  m;
        }
        return sum;
    }
}
```