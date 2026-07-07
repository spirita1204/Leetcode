# 3754. Concatenate Non-Zero Digits and Multiply by Sum I  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>You are given an integer `n`.

Form a new integer `x` by concatenating all the **non-zero digits** of `n` in their original order. If there are no **non-zero** digits, `x = 0`.

Let `sum` be the **sum of digits** in `x`.

Return an integer representing the value of `x * sum`.

**Example 1:**

**Input:** n = 10203004

**Output:** 12340

**Explanation:**

- The non-zero digits are 1, 2, 3, and 4. Thus, `x = 1234`.
- The sum of digits is `sum = 1 + 2 + 3 + 4 = 10`.
- Therefore, the answer is `x * sum = 1234 * 10 = 12340`.
**Example 2:**

**Input:** n = 1000

**Output:** 1

**Explanation:  **

- The non-zero digit is 1, so `x = 1` and `sum = 1`.
- Therefore, the answer is `x * sum = 1 * 1 = 1`. 
**Constraints:   **

- `0 <= n <= 109`
```go
func sumAndMultiply(n int) int64 {
    var x int64 = 0
    var sum int64 = 0
  
    divisor := 1
    for n/divisor >= 10 {
        divisor *= 10
    }

    for divisor > 0 {
        digit := n / divisor
        n %= divisor
        if digit != 0 {
            x = x*10 + int64(digit)
            sum += int64(digit)
        }
        divisor /= 10
    }
    return x * sum
}
```



