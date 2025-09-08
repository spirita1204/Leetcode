# 1317. Convert Integer to the Sum of Two No-Zero Integers  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>**No-Zero integer** is a positive integer that **does not contain any **`**0**` in its decimal representation.

Given an integer `n`, return *a list of two integers* `[a, b]` *where*:

- `a` and `b` are **No-Zero integers**.   
- `a + b = n`
The test cases are generated so that there is at least one valid solution. If there are many valid solutions, you can return any of them.

**Example 1:**

```plain text
Input: n = 2
Output: [1,1]
Explanation: Let a = 1 and b = 1.
Both a and b are no-zero integers, and a + b = 2 = n.
```

**Example 2:**

```plain text
Input: n = 11
Output: [2,9]
Explanation: Let a = 2 and b = 9.
Both a and b are no-zero integers, and a + b = 11 = n.
Note that there are other valid answers as [8, 3] that can be accepted.
```

**Constraints:**

- `2 <= n <= 104`
```java
class Solution {
    public int[] getNoZeroIntegers(int n) {
        for(int i = 1; i < n; i++) {
            if(!String.valueOf(i).contains("0") &&
                !String.valueOf(n - i).contains("0"))
                return new int[]{i, n - i};
        }
        return null;
    }
}
```

