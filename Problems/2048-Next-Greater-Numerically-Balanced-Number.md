# 2048. Next Greater Numerically Balanced Number  

  Methods: DFS </br> Difficulty: Medium </br> </br>An integer `x` is **numerically balanced** if for every digit `d` in the number `x`, there are **exactly** `d` occurrences of that digit in `x`.

Given an integer `n`, return *the ****smallest numerically balanced**** number ****strictly greater**** than *`n`*.*

**Example 1:**

```plain text
Input: n = 1
Output: 22
Explanation:
22 is numerically balanced since:
- The digit 2 occurs 2 times.
It is also the smallest numerically balanced number strictly greater than 1.
```

**Example 2:**

```plain text
Input: n = 1000
Output: 1333
Explanation:
1333 is numerically balanced since:
- The digit 1 occurs 1 time.
- The digit 3 occurs 3 times.
It is also the smallest numerically balanced number strictly greater than 1000.
Note that 1022 cannot be the answer because 0 appeared more than 0 times.
```

**Example 3:**

```plain text
Input: n = 3000
Output: 3133
Explanation:
3133 is numerically balanced since:
- The digit 1 occurs 1 time.
- The digit 3 occurs 3 times.
It is also the smallest numerically balanced number strictly greater than 3000.
```

**Constraints:**

- `0 <= n <= 106`
```java
class Solution {
    public int nextBeautifulNumber(int n) {
        List<Integer> list = new ArrayList<>();
        generate(0, new int[10], list);
        Collections.sort(list);
        for (int num : list) {
            if (num > n) return num;
        }
        return -1;
    }

    private void generate(long num, int[] count, List<Integer> list) {
        if (num > 0 && isBeautiful(count)) {
            list.add((int) num);
        }
        if (num > 1224444) return;

        for (int d = 1; d <= 7; d++) {
            if (count[d] < d) {
                count[d]++;
                generate(num * 10 + d, count, list);
                count[d]--;
            }
        }
    }
    private boolean isBeautiful(int[] count) {
        for (int d = 1; d <= 7; d++) {
            if (count[d] != 0 && count[d] != d) 
                return false;
        }
        return true;
    }
}
```

