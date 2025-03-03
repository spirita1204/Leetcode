# 2161. Partition Array According to Given Pivot  

  Methods: Array </br> Difficulty: Medium </br> </br>You are given a **0-indexed** integer array `nums` and an integer `pivot`. Rearrange `nums` such that the following conditions are satisfied:

- Every element less than `pivot` appears **before** every element greater than `pivot`.
- Every element equal to `pivot` appears **in between** the elements less than and greater than `pivot`.
- The **relative order** of the elements less than `pivot` and the elements greater than `pivot` is maintained.
Return `nums`* after the rearrangement.*

**Example 1:**

```plain text
Input: nums = [9,12,5,10,14,3,10], pivot = 10
Output: [9,5,3,10,10,12,14]
Explanation:
The elements 9, 5, and 3 are less than the pivot so they are on the left side of the array.
The elements 12 and 14 are greater than the pivot so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [9, 5, 3] and [12, 14] are the respective orderings.

```

**Example 2:**

```plain text
Input: nums = [-3,4,3,2], pivot = 2
Output: [-3,2,4,3]
Explanation:
The element -3 is less than the pivot so it is on the left side of the array.
The elements 4 and 3 are greater than the pivot so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [-3] and [4, 3] are the respective orderings.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `106 <= nums[i] <= 106`
- `pivot` equals to an element of `nums`. 
```java
class Solution {
    public int[] pivotArray(int[] nums, int pivot) {
        List<Integer> left = new ArrayList<>();
        List<Integer> right = new ArrayList<>();
        int midCnt = 0;
        for(int num: nums) {
            if(num < pivot) 
                left.add(num);
            if(num > pivot)
                right.add(num);
            if(num == pivot)
                midCnt++;
        }
        int[] res = new int[nums.length];
        int p1 = 0, p2 = 0, idx = 0;
        while(p1 < left.size())
            res[idx++] = left.get(p1++);
        while(midCnt-- > 0)
            res[idx++] = pivot;
        while(p2 < right.size())
            res[idx++] = right.get(p2++);
            
        return res;
    }
}
```

優化 用Array 處理就好 

```java
class Solution {
    public int[] pivotArray(int[] nums, int pivot) {
        int n = nums.length;

        int[] less = new int[n];
        int[] high = new int[n];
        int[] result = new int[n];

        // Counters for different parts of the array
        int count = 0; // To count the number of pivot elements
        int j = 0; // Index for the 'less' array
        int k = 0; // Index for the 'high' array

        // Partition the input array into 'less', 'high', and count pivot occurrences
        for (int i = 0; i < n; i++) {
            if (nums[i] < pivot) {
                less[j++] = nums[i];
            } else if (nums[i] == pivot) {
                count++;
            } else {
                high[k++] = nums[i];
            }
        }

        // Fill the result array
        int index = 0;

        // Add elements less than the pivot
        for (int a = 0; a < j; a++) {
            result[index++] = less[a];
        }

        // Add the pivot element `count` times
        for (int a = 0; a < count; a++) {
            result[index++] = pivot;
        }

        // Add elements greater than the pivot
        for (int a = 0; a < k; a++) {
            result[index++] = high[a];
        }

        return result;
    }
}
```

