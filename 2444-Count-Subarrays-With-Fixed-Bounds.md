# 2444. Count Subarrays With Fixed Bounds

Methods: Pointer
Difficulty: Hard

[https://www.youtube.com/watch?v=aekkfcxEWYY](https://www.youtube.com/watch?v=aekkfcxEWYY)

![Untitled](Untitled%2016.png)

You are given an integer array `nums` and two integers `minK` and `maxK`.

A **fixed-bound subarray** of `nums` is a subarray that satisfies the following conditions:

- The **minimum** value in the subarray is equal to `minK`.
- The **maximum** value in the subarray is equal to `maxK`.

Return *the **number** of fixed-bound subarrays*.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

```
Input: nums = [1,3,5,2,7,5], minK = 1, maxK = 5
Output: 2
Explanation: The fixed-bound subarrays are [1,3,5] and [1,3,5,2].

```

**Example 2:**

```
Input: nums = [1,1,1,1], minK = 1, maxK = 1
Output: 10
Explanation: Every subarray of nums is a fixed-bound subarray. There are 10 possible subarrays.
```

```java
class Solution {
    public long countSubarrays(int[] nums, int minK, int maxK) {
        int left = 0;//定義可以到左的點
        int lastMin = -1, lastMax = -1;
        int n = nums.length;
        long res = 0L;
        for(int right = 0 ; right < n; right++){
            if(nums[right]<minK || nums[right]>maxK){//超出邊界
                lastMin = -1;
                lastMax = -1;
                left = right+1;
            }
            if(nums[right]==minK) lastMin = right;
            if(nums[right]==maxK) lastMax = right;
            //當min max都有 取他們最小(Math.min)代表最少要有subarr的長度 減掉可以繼續往左延伸的距離 就是subarr可以的數量
            if(lastMin!=-1 && lastMax!=-1) res += Math.min(lastMin, lastMax)-left+1;
        }
        return res;
    }
}
```