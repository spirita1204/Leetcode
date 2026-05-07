# 3660. Jump Game IX  

  Methods: Pointer,Prefix Sum </br> </br>You are given an integer array `nums`.

From any index `i`, you can jump to another index `j` under the following rules:

- Jump to index `j` where `j > i` is allowed only if `nums[j] < nums[i]`.
- Jump to index `j` where `j < i` is allowed only if `nums[j] > nums[i]`.
For each index `i`, find the **maximum** **value** in `nums` that can be reached by following **any** sequence of valid jumps starting at `i`.

Return an array `ans` where `ans[i]` is the **maximum** **value** reachable starting from index `i`.

**Example 1:**

**Input:** nums = [2,1,3]

**Output:** [2,2,3]

**Explanation:**

- For `i = 0`: No jump increases the value.
- For `i = 1`: Jump to `j = 0` as `nums[j] = 2` is greater than `nums[i]`.
- For `i = 2`: Since `nums[2] = 3` is the maximum value in `nums`, no jump increases the value.
Thus, `ans = [2, 2, 3]`.

**Example 2:**

**Input:** nums = [2,3,1]

**Output:** [3,3,3] 

**Explanation:**

- For `i = 0`: Jump forward to `j = 2` as `nums[j] = 1` is less than `nums[i] = 2`, then from `i = 2` jump to `j = 1` as `nums[j] = 3` is greater than `nums[2]`.
- For `i = 1`: Since `nums[1] = 3` is the maximum value in `nums`, no jump increases the value.   
- For `i = 2`: Jump to `j = 1` as `nums[j] = 3` is greater than `nums[2] = 1`.
Thus, `ans = [3, 3, 3]`.

**Constraints:**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 109`
```go
func maxValue(nums []int) []int {
	n := len(nums)

	suffixMin := make([]int, n+1)
    // 預設最大值
	suffixMin[n] = int(^uint(0) >> 1)
    // 1 1 3 max
	for i := n - 1; i >= 0; i-- {
		if nums[i] < suffixMin[i+1] {
			suffixMin[i] = nums[i]
		} else {
			suffixMin[i] = suffixMin[i+1]  
		}
	}

	ans := make([]int, n)
	l := 0

	for l < n {
		r := l
		componentMax := nums[l]
        // 右邊還有更小的數
		for r+1 < n && componentMax > suffixMin[r+1] {
			r++
			if nums[r] > componentMax {
				componentMax = nums[r]
			}
		}

		for i := l; i <= r; i++ {
			ans[i] = componentMax
		}

		l = r + 1
	}

	return ans
}
```

