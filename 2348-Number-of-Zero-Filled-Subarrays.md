# 2348. Number of Zero-Filled Subarrays

Methods: Pointer
Difficulty: Medium

Given an integer array `nums`, return *the number of **subarrays** filled with* `0`.

A **subarray** is a contiguous non-empty sequence of elements within an array.

**Example 1:**

```
Input: nums = [1,3,0,0,2,0,0,4]
Output: 6
Explanation:
There are 4 occurrences of [0] as a subarray.
There are 2 occurrences of [0,0] as a subarray.
There is no occurrence of a subarray with a size more than 2 filled with 0. Therefore, we return 6.
```

**Example 2:**

```
Input: nums = [0,0,0,2,0,0]
Output: 9
Explanation:
There are 5 occurrences of [0] as a subarray.
There are 3 occurrences of [0,0] as a subarray.
There is 1 occurrence of [0,0,0] as a subarray.
There is no occurrence of a subarray with a size more than 3 filled with 0. Therefore, we return 9.

```

**Example 3:**

```
Input: nums = [2,10,2019]
Output: 0
Explanation: There is no subarray filled with 0. Therefore, we return 0.

```

**Constraints:**

- `1 <= nums.length <= 105`
- `109 <= nums[i] <= 109`

**太攏長**

```json
class Solution {
    public long zeroFilledSubarray(int[] nums) {
        if(nums.length == 1){
            if(nums[0] == 0) return 1;
            else return 0;
        }
        long[] sub = new long[nums.length/2 + 1]; //最多有多少個subArray
        long contig = 0; // 計算最常相連
        int index = 0; // subarray長度填入sub中
        long res = 0; 
        for(int i = 0; i < nums.length; i++){
            if(i == nums.length - 1){
                if(nums[i] == 0){
                    contig++;
                    sub[index] = contig;
                }else
                    sub[index] = contig;
                break;
            }
            if(nums[i] == 0) contig++;
            else{
                if(contig == 0) continue;
                sub[index] = contig;
                index++;
                contig = 0;
            }
        }
        for(long num : sub){
            if(num == 0) continue;
            System.out.println(count(num));
            res += count(num);
        }
        return res;
    }
    public long count(long num){ // 計算子array可以以多少組合
        return  (1+ num)* num/ 2;
    } 
}
```

Best method

[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/number-of-zero-filled-subarrays/solutions/2322338/two-pointers/?orderBy=most_votes)

```json

public long zeroFilledSubarray(int[] nums) {
    long res = 0;
    for (int i = 0, j = 0; i < nums.length; ++i) {
        if (nums[i] != 0)
            j = i + 1;
         res += i - j + 1;
    }
    return res;
}
```