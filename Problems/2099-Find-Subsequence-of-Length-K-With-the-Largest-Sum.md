# 2099. Find Subsequence of Length K With the Largest Sum  

  Data Structure: Heap </br> Difficulty: Easy </br> </br>You are given an integer array `nums` and an integer `k`. You want to find a **subsequence **of `nums` of length `k` that has the **largest** sum.   

Return* ****any**** such subsequence as an integer array of length *`k`.

A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

**Example 1:**

```plain text
Input: nums = [2,1,3,3], k = 2
Output: [3,3]
Explanation:
The subsequence has the largest sum of 3 + 3 = 6.
```

**Example 2:**

```plain text
Input: nums = [-1,-2,3,4], k = 3
Output: [-1,3,4]
Explanation:
The subsequence has the largest sum of -1 + 3 + 4 = 6.
```

**Example 3:**

```plain text
Input: nums = [3,4,3,3], k = 2
Output: [3,4]
Explanation:
The subsequence has the largest sum of 3 + 4 = 7.
Another possible subsequence is [4, 3].
```

**Constraints:**

- `1 <= nums.length <= 1000`
- `105 <= nums[i] <= 105`
- `1 <= k <= nums.length`
```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        // val , idx
        Queue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        Queue<int[]> pq2 = new PriorityQueue<>((a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        int[] res = new int[k];
        int n = nums.length - k;

        for(int i = 0; i < nums.length; i++) 
            pq.offer(new int[]{nums[i], i});

        while(n-- > 0) 
           pq.poll();

        while(!pq.isEmpty()){
            int[] e = pq.poll();
            pq2.offer(new int[]{e[1], e[0]});
        }
           
        int i = 0;
        while(!pq2.isEmpty()) 
            res[i++] = pq2.poll()[1];
        
        return res;
    }
}
```

