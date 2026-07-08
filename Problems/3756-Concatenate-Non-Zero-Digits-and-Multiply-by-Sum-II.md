# 3756. Concatenate Non-Zero Digits and Multiply by Sum II  

  Methods: Prefix Sum </br> Difficulty: Medium </br> </br>You are given a string `s` of length `m` consisting of digits. You are also given a 2D integer array `queries`, where `queries[i] = [li, ri]`.

For each `queries[i]`, extract the **substring** `s[li..ri]`. Then, perform the following:

- Form a new integer `x` by concatenating all the **non-zero digits** from the substring in their original order. If there are no non-zero digits, `x = 0`.   
- Let `sum` be the **sum of digits** in `x`. The answer is `x * sum`.
Return an array of integers `answer` where `answer[i]` is the answer to the `ith` query.

Since the answers may be very large, return them **modulo** `109 + 7`.

**Example 1:**

**Input:** s = "10203004", queries = [[0,7],[1,3],[4,6]]

**Output:** [12340, 4, 9]  

**Explanation:**

- `s[0..7] = "10203004"`
- `s[1..3] = "020"`
- `s[4..6] = "300"`
**Example 2:**

**Input:** s = "1000", queries = [[0,3],[1,1]]

**Output:** [1, 0]

**Explanation:**

- `s[0..3] = "1000"`
- `s[1..1] = "0"`
**Example 3:**

**Input:** s = "9876543210", queries = [[0,9]]

**Output:** [444444137]

**Explanation:**

- `s[0..9] = "9876543210"`
**Constraints:**

- `1 <= m == s.length <= 105`
- `s` consists of digits only.
- `1 <= queries.length <= 105`
- `queries[i] = [li, ri]`
- `0 <= li <= ri < m`
```go
func sumAndMultiply(s string, queries [][]int) []int {
    const MOD int64 = 1000000007
    n := len(s)
    nonZeroCount := make([]int, n+1)// 0 1 1 2 2 3 3 4
    digits := make([]int64, 0, n)// 1234

    for i := 0; i < n; i++ {
        nonZeroCount[i+1] = nonZeroCount[i]    

        if s[i] != '0' {
            nonZeroCount[i+1]++
            digits = append(digits, int64(s[i]-'0'))
        }
    }   

    k := len(digits)

    prefixValue := make([]int64, k+1)// 1 12 123 1234
    prefixSum := make([]int64, k+1)// 0 1 3 6 10
    power10 := make([]int64, k+1)// 1 10 100 1000
    power10[0] = 1

    for i := 0; i < k; i++ {
        prefixValue[i+1] = (prefixValue[i]*10 + digits[i]) % MOD
        prefixSum[i+1] = prefixSum[i] + digits[i]
        power10[i+1] = (power10[i] * 10) % MOD
    }  

    answer := make([]int, len(queries))  

    for i, query := range queries {
        l := query[0]  
        r := query[1]

        left := nonZeroCount[l]
        right := nonZeroCount[r+1]
        length := right - left
        
        x := (prefixValue[right] - (prefixValue[left]*power10[length])%MOD + MOD) % MOD
        sum := prefixSum[right] - prefixSum[left]
        answer[i] = int((x * sum) % MOD)
    }

    return answer
}
```



