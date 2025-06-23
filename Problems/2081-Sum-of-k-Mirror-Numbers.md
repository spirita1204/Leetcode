# 2081. Sum of k-Mirror Numbers  

  Methods: Basic logic </br> Difficulty: Hard </br> </br>A **k-mirror number** is a **positive** integer **without leading zeros** that reads the same both forward and backward in base-10 **as well as** in base-k.

- For example, `9` is a 2-mirror number. The representation of `9` in base-10 and base-2 are `9` and `1001` respectively, which read the same both forward and backward.
- On the contrary, `4` is not a 2-mirror number. The representation of `4` in base-2 is `100`, which does not read the same both forward and backward.
Given the base `k` and the number `n`, return *the ****sum**** of the* `n` ***smallest**** k-mirror numbers*.

**Example 1:**

```plain text
Input: k = 2, n = 5
Output: 25
Explanation:
The 5 smallest 2-mirror numbers and their representations in base-2 are listed as follows:
  base-10    base-2 
    1          1
    3          11
    5          101
    7          111
    9          1001
Their sum = 1 + 3 + 5 + 7 + 9 = 25.
```

**Example 2:**

```plain text
Input: k = 3, n = 7
Output: 499
Explanation:
The 7 smallest 3-mirror numbers are and their representations in base-3 are listed as follows:
  base-10    base-3
    1          1
    2          2
    4          11
    8          22
    121        11111
    151        12121
    212        21212
Their sum = 1 + 2 + 4 + 8 + 121 + 151 + 212 = 499.
```

**Example 3:**

```plain text
Input: k = 7, n = 17
Output: 20379000
Explanation: The 17 smallest 7-mirror numbers are:
1, 2, 3, 4, 5, 6, 8, 121, 171, 242, 292, 16561, 65656, 2137312, 4602064, 6597956, 6958596
```

**Constraints:**

- `2 <= k <= 9`
- `1 <= n <= 30`
```java
class Solution {
    public long kMirror(int k, int n) {
        long res = 0;

        for (long len = 1; n > 0; len *= 10) {
            // 第一個迴圈：遍歷奇數長度的回文數字
            for (long i = len; n > 0 && i < len * 10; i++) {
                long p = createPalindrome(i, true); // 創建奇數長度的回文數字
                if (isPalindrome(p, k)) { 
                    res += p;
                    n--;
                }
            }
            // 第二個迴圈：遍歷偶數長度的回文數字
            for (long i = len; n > 0 && i < len * 10; i++) {
                long p = createPalindrome(i, false); // 創建偶數長度的回文數字
                if (isPalindrome(p, k)) { 
                    res += p;
                    n--;
                }
            }
        }

        return res;
    }

    private long createPalindrome(long num, boolean odd) {
        long x = num;

        if (odd)
            x /= 10;
        while (x > 0) {
            num = num * 10 + x % 10;
            x /= 10;
        }
        return num;
    }

    private boolean isPalindrome(long num, int base) {
        StringBuilder sb = new StringBuilder();

        while (num > 0) {
            sb.append((char) (num % base + '0'));
            num /= base;
        }
        String s = sb.toString();
        int i = 0, j = s.length() - 1;

        while (i < j)
            if (s.charAt(i++) != s.charAt(j--))
                return false;

        return true;
    }

}
```

