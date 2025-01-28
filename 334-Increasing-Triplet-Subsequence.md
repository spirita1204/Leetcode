# 334. Increasing Triplet Subsequence

Methods: DP
Difficulty: Medium

**Medium**

6.3K

276

Companies

Given an integer array `nums`, return `true` *if there exists a triple of indices* `(i, j, k)` *such that* `i < j < k` *and* `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

**Example 1:**

```
Input: nums = [1,2,3,4,5]
Output: true
Explanation: Any triplet where i < j < k is valid.

```

**Example 2:**

```
Input: nums = [5,4,3,2,1]
Output: false
Explanation: No triplet exists.

```

**Example 3:**

```
Input: nums = [2,1,5,0,4,6]
Output: true
Explanation: The triplet (3, 4, 5) is valid because nums[3] == 0 < nums[4] == 4 < nums[5] == 6.

```

**Constraints:**

- `1 <= nums.length <= 5 * 105`
- `231 <= nums[i] <= 231 - 1`

**Follow up:**

Could you implement a solution that runs in

```
O(n)
```

time complexity and

```
O(1)
```

space complexity?

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
		int[] tails = new int[nums.length];//紀錄不同長度下末端最優解
		int size = 0;

		for (int x : nums) {
			int left = 0, right = size;
			while (left < right) {
				int m = (left + right) / 2;
				if (tails[m] < x)//往後延伸
					left = m + 1;
				else
					right = m;//當比較小 可以以它作為結尾 更憂解
			}
			tails[left] = x;
			if (left == size) ++size;
		}
		return (size >= 3) ? true: false;  
    }
}
```