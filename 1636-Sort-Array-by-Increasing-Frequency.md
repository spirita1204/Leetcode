# 1636. Sort Array by Increasing Frequency

Methods: Basic logic
Difficulty: Easy

Easy

Topics

Companies

Hint

Given an array of integers `nums`, sort the array in **increasing** order based on the frequency of the values. If multiple values have the same frequency, sort them in **decreasing** order.

Return the *sorted array*.

**Example 1:**

```
Input: nums = [1,1,2,2,2,3]
Output: [3,1,1,2,2,2]
Explanation: '3' has a frequency of 1, '1' has a frequency of 2, and '2' has a frequency of 3.

```

**Example 2:**

```
Input: nums = [2,3,1,3,2]
Output: [1,3,3,2,2]
Explanation: '2' and '3' both have a frequency of 2, so they are sorted in decreasing order.

```

**Example 3:**

```
Input: nums = [-1,1,-6,4,5,-6,1,4,1]
Output: [5,-1,4,4,-6,-6,1,1,1]
```

**Constraints:**

- `1 <= nums.length <= 100`
- `100 <= nums[i] <= 100`

```java
class Solution {
    public int[] frequencySort(int[] nums) {
        int len = nums.length;
        int[] res = new int[len];
        int[][] eCnts = new int[201][2];
        for (int i = 0; i < len; i++) {
            eCnts[nums[i] + 100][0] = nums[i];
            eCnts[nums[i] + 100][1]++;
        }
        Arrays.sort(eCnts, (a, b) -> ((a[1] == b[1]) ? b[0] - a[0] : a[1] - b[1])); 
        int idx = 0;
        for (int i = 0; i < eCnts.length; i++) {
            if (eCnts[i][1] != 0) {
                for (int j = 0; j < eCnts[i][1]; j++) {
                    res[idx++] = eCnts[i][0];
                }
            }
        }
        return res;
    }
}
```