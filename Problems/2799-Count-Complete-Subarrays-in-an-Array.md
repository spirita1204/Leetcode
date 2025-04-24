# 2799. Count Complete Subarrays in an Array  

  Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given an array `nums` consisting of **positive** integers.

We call a subarray of an array **complete** if the following condition is satisfied:

- The number of **distinct** elements in the subarray is equal to the number of distinct elements in the whole array.
Return *the number of ****complete**** subarrays*.

A **subarray** is a contiguous non-empty part of an array.

**Example 1:**

```plain text
Input: nums = [1,3,1,2,2]
Output: 4
Explanation: The complete subarrays are the following: [1,3,1,2], [1,3,1,2,2], [3,1,2] and [3,1,2,2].
```

**Example 2:**

```plain text
Input: nums = [5,5,5,5]
Output: 10
Explanation: The array consists only of the integer 5, so any subarray is complete. The number of subarrays that we can choose is 10.
```

**Constraints:**

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 2000`


O(N^2)

```java
class Solution {
    public int countCompleteSubarrays(int[] nums) {
        int res = 0;
        int distinctCnt = 0;
        int len = nums.length;
        int[] vis = new int[2001];

        for(int i = 0; i < len; i++) 
            vis[nums[i]]++;

        for(int i = 0; i < 2001; i++)
            if(vis[i] != 0) 
                distinctCnt++;

        for (int i = 0; i < len; i++) {
            Set<Integer> st = new HashSet<>();
            for (int j = i; j < len; j++) {
                st.add(nums[j]);
                if (st.size() == distinctCnt)
                    res++;
            }
        }
        return res;
    }
}
```

Sliding Window O(N)

```java
class Solution {
    public int countCompleteSubarrays(int[] nums) {
        int p1 = 0, res = 0;
        int k = (int) Arrays.stream(nums).distinct().count();

        Map<Integer, Integer> hm = new HashMap<>();
        int len = nums.length;

        for (int p2 = 0; p2 < len; p2++) {
            hm.put(nums[p2], hm.getOrDefault(nums[p2], 0) + 1);
            while (hm.size() == k) {
                res += (len - p2);
                // 右移
                hm.put(nums[p1], hm.get(nums[p1]) - 1);
                if (hm.get(nums[p1]) == 0) 
                    hm.remove(nums[p1]);
                p1++;
            }
        }
        return res;
    }
}
```

