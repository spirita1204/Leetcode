# 3629. Minimum Jumps to Reach End via Prime Teleportation  

  Methods: BFS </br> Difficulty: Medium </br> </br>You are given an integer array `nums` of length `n`.

You start at index 0, and your goal is to reach index `n - 1`.

From any index `i`, you may perform one of the following operations:

- **Adjacent Step**: Jump to index `i + 1` or `i - 1`, if the index is within bounds.
- **Prime Teleportation**: If `nums[i]` is a  `p`, you may instantly jump to any index `j != i` such that `nums[j] % p == 0`.
Return the **minimum** number of jumps required to reach index `n - 1`.

**Example 1:**

**Input:** nums = [1,2,4,6]

**Output:** 2

**Explanation:**

One optimal sequence of jumps is:

- Start at index `i = 0`. Take an adjacent step to index 1.
- At index `i = 1`, `nums[1] = 2` is a prime number. Therefore, we teleport to index `i = 3` as `nums[3] = 6` is divisible by 2.
Thus, the answer is 2.

**Example 2:**

**Input:** nums = [2,3,4,7,9]

**Output:** 2

**Explanation:**

One optimal sequence of jumps is:

- Start at index `i = 0`. Take an adjacent step to index `i = 1`.
- At index `i = 1`, `nums[1] = 3` is a prime number. Therefore, we teleport to index `i = 4` since `nums[4] = 9` is divisible by 3.
Thus, the answer is 2.

**Example 3:**

**Input:** nums = [4,6,5,8]

**Output:** 3

**Explanation:**

- Since no teleportation is possible, we move through `0 → 1 → 2 → 3`. Thus, the answer is 3.
**Constraints:    **

- `1 <= n == nums.length <= 105`
- `1 <= nums[i] <= 106`
```go
func minJumps(nums []int) int {

	n := len(nums)

	if n == 1 {
		return 0
	}

	mx := 0
    // 尋找最大值與預處理質數因數 (埃拉托斯特尼篩法)
	for _, x := range nums {
		if x > mx {
			mx = x
		}
	}

	spf := make([]int, mx+1)

	for i := 0; i <= mx; i++ {
		spf[i] = i
	}
    // spf[x] 儲存數字 x 的最小質因數 
    // ex: spf[6] = 2, spf[9] = 3
	for i := 2; i*i <= mx; i++ {
		if spf[i] == i {
			for j := i * i; j <= mx; j += i {
				if spf[j] == j {
					spf[j] = i
				}
			}
		}
	}
    // 建立「質數對應索引」的 Mapping 2->(1,2,3) 質數->索引
	mp := map[int][]int{}

	for i, val := range nums {
		x := val
		used := map[int]bool{}// 當前數字處理過哪些質因數
		for x > 1 {
			p := spf[x]
			if !used[p] {
				mp[p] = append(mp[p], i)
				used[p] = true
			}
			x /= p
		}
	}
    // BFS
	q := []int{0}
	dist := make([]int, n)// 記錄從起點走到每個索引需要的最少步數

	for i := 0; i < n; i++ {
		dist[i] = -1
	}

	dist[0] = 0
	front := 0

	for front < len(q) {
		i := q[front]
		front++
		steps := dist[i]// 走到目前位置 i 所累積的步數

		if i == n-1 {// 廣度優先最快走到就是解
			return steps
		}
        // 往左走一步
		if i-1 >= 0 && dist[i-1] == -1 {
			dist[i-1] = steps + 1
			q = append(q, i-1)
		}
        // 往右走一步
		if i+1 < n && dist[i+1] == -1 {
			dist[i+1] = steps + 1
			q = append(q, i+1)
		}
        // 質數傳送
		val := nums[i]

		if val > 1 && spf[val] == val {// 是質數
			for _, nxt := range mp[val] {
				if dist[nxt] == -1 {
					dist[nxt] = steps + 1
					q = append(q, nxt)
				}
			}
            // 清空這個質數的清單 優化 省時間
			mp[val] = []int{}
		}
	}
	return -1
}
```



