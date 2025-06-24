# 2200. Find All K-Distant Indices in an Array  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given a **0-indexed** integer array `nums` and two integers `key` and `k`. A **k-distant index** is an index `i` of `nums` for which there exists at least one index `j` such that `|i - j| <= k` and `nums[j] == key`.

Return *a list of all k-distant indices sorted in ****increasing order***.  

**Example 1:**

```plain text
Input: nums = [3,4,9,1,3,9,5], key = 9, k = 1
Output: [1,2,3,4,5,6]
Explanation: Here,nums[2] == key andnums[5] == key.
- For index 0, |0 - 2| > k and |0 - 5| > k, so there is no j where|0 - j| <= k andnums[j] == key. Thus, 0 is not a k-distant index.
- For index 1, |1 - 2| <= k and nums[2] == key, so 1 is a k-distant index.
- For index 2, |2 - 2| <= k and nums[2] == key, so 2 is a k-distant index.
- For index 3, |3 - 2| <= k and nums[2] == key, so 3 is a k-distant index.
- For index 4, |4 - 5| <= k and nums[5] == key, so 4 is a k-distant index.
- For index 5, |5 - 5| <= k and nums[5] == key, so 5 is a k-distant index.
- For index 6, |6 - 5| <= k and nums[5] == key, so 6 is a k-distant index.
Thus, we return [1,2,3,4,5,6] which is sorted in increasing order.
```

**Example 2:**

```plain text
Input: nums = [2,2,2,2,2], key = 2, k = 2
Output: [0,1,2,3,4]
Explanation: For all indices i in nums, there exists some index j such that |i - j| <= k and nums[j] == key, so every index is a k-distant index.
Hence, we return [0,1,2,3,4].
```

**Constraints:**

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 1000`
- `key` is an integer from the array `nums`.
- `1 <= k <= nums.length`
```java
class Solution {
    public List<Integer> findKDistantIndices(int[] nums, int key, int k) {
        List<Integer> list = new ArrayList<>();
        HashSet<Integer> hs = new HashSet<>();

        for(int i = 0; i < nums.length; i++) 
            if(nums[i] == key)  
                list.add(i);
        
        for(int i = 0; i < nums.length; i++) 
            for(int j : list) 
                if(Math.abs(i - j) <= k)
                    hs.add(i);
            
        List<Integer> res = new ArrayList<>(hs);
        Collections.sort(res);

        return res;
    }
}
```

