# 1432. Max Difference You Can Get From Changing an Integer  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given an integer `num`. You will apply the following steps to `num` **two** separate times:

- Pick a digit `x (0 <= x <= 9)`. 
- Pick another digit `y (0 <= y <= 9)`. Note `y` can be equal to `x`.
- Replace all the occurrences of `x` in the decimal representation of `num` by `y`.
Let `a` and `b` be the two results from applying the operation to `num` *independently*.

Return *the max difference* between `a` and `b`. 

Note that neither `a` nor `b` may have any leading zeros, and **must not** be 0.

**Example 1:**

```plain text
Input: num = 555
Output: 888
Explanation: The first time pick x = 5 and y = 9 and store the new integer in a.
The second time pick x = 5 and y = 1 and store the new integer in b.
We have now a = 999 and b = 111 and max difference = 888
```

**Example 2:**

```plain text
Input: num = 9
Output: 8
Explanation: The first time pick x = 9 and y = 9 and store the new integer in a.
The second time pick x = 9 and y = 1 and store the new integer in b.
We have now a = 9 and b = 1 and max difference = 8
```

**Constraints:**

- `1 <= num <= 108`
```java
class Solution {
    public int maxDiff(int num) {
        String str = Integer.toString(num);
        StringBuilder maxStr = new StringBuilder(str);
        StringBuilder minStr = new StringBuilder(str);

        char maxDigit = ' ';
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) != '9') {
                maxDigit = str.charAt(i);
                break;
            }
        }

        if (maxDigit != ' ') {
            for (int i = 0; i < maxStr.length(); i++) {
                if (maxStr.charAt(i) == maxDigit) {
                    maxStr.setCharAt(i, '9');
                }
            }
        }
        char minDigit = str.charAt(0);
        char replace = '1';

        if (minDigit == '1') {
            for (int i = 1; i < str.length(); i++) {
                if (str.charAt(i) != '0' && str.charAt(i) != '1') {
                    minDigit = str.charAt(i);
                    replace = '0';
                    break;
                }
            }
        }

        for (int i = 0; i < minStr.length(); i++) {
            if (minStr.charAt(i) == minDigit) {
                minStr.setCharAt(i, replace);
            }
        }

        int maxVal = Integer.parseInt(maxStr.toString());
        int minVal = Integer.parseInt(minStr.toString());

        return maxVal - minVal;
    }
}
```

