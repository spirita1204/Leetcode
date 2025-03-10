# 441. Arranging Coins

Methods: Binary Search
Difficulty: Easy

**Easy**

3.2K

1.2K

Companies

You have `n` coins and you want to build a staircase with these coins. The staircase consists of `k` rows where the `ith` row has exactly `i` coins. The last row of the staircase **may be** incomplete.

Given the integer `n`, return *the number of **complete rows** of the staircase you will build*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/04/09/arrangecoins1-grid.jpg](https://assets.leetcode.com/uploads/2021/04/09/arrangecoins1-grid.jpg)

```
Input: n = 5
Output: 2
Explanation: Because the 3rd row is incomplete, we return 2.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/04/09/arrangecoins2-grid.jpg](https://assets.leetcode.com/uploads/2021/04/09/arrangecoins2-grid.jpg)

```
Input: n = 8
Output: 3
Explanation: Because the 4th row is incomplete, we return 3.

```

**Constraints:**

- `1 <= n <= 231 - 1`

```java
class Solution {
	/* Interate
	public int arrangeCoins(int n) {
    int i = 1;
    int res = 0;
    while(n - i >= 0){
      n = n - i;
      i++;
      res++;
    }
    return res;
  }
	*/
  public int arrangeCoins(int n) {
		long left = 0; // we use "long" because we may get an integer overflow
		long right = n;
		while(left <= right){
			long pivot = left + (right - left) / 2;
			long coinsUsed = pivot * (pivot + 1)/2;
			if(coinsUsed == n){
				return (int)pivot;
			}
			if(n < coinsUsed){
				right = pivot-1;
			}
			else{
				left = pivot + 1;
			}
		}
		return (int)right; // cast as an "int" because it was initiliazed as a "long"
  }
}
```