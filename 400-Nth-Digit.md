# 400. Nth Digit

Methods: Basic logic
Difficulty: Medium

Medium

Topics

Companies

Given an integer `n`, return the `nth` digit of the infinite integer sequence `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...]`.

**Example 1:**

```
Input: n = 3
Output: 3

```

**Example 2:**

```
Input: n = 11
Output: 0
Explanation: The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.

```

**Constraints:**

- `1 <= n <= 231 - 1`

```java
class Solution {
	public int findNthDigit(int n) {
        // 1 ~ 9 include 9 one digit number;
        // 10 ~ 99 include 90 two digits number;
        // 100 ~ 999 include 900 three digits number;
        // 1000 ~ 9999 include 9000 four digits number;
		int len = 1;// 多少數字
        int i = 1;
		long range = 9;// 9 90 900...
		while(n > len * range){
			n -= len * range;
			len++;// 一位 兩位...
			range *= 10;
			i *= 10;// 從哪個 起始點開始
		}
		i += (n - 1) / len;// 在789數字中哪位
		String s = Integer.toString(i);
		return Character.getNumericValue(s.charAt((n - 1) % len));// 取當前數字的第k位
	}
}
```