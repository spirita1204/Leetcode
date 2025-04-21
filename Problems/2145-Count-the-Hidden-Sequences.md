# 2145. Count the Hidden Sequences  

  Methods: Math,Basic logic </br> Difficulty: Medium </br> </br>You are given a **0-indexed** array of `n` integers `differences`, which describes the **differences **between each pair of **consecutive **integers of a **hidden** sequence of length `(n + 1)`. More formally, call the hidden sequence `hidden`, then we have that `differences[i] = hidden[i + 1] - hidden[i]`.

You are further given two integers `lower` and `upper` that describe the **inclusive** range of values `[lower, upper]` that the hidden sequence can contain.

- For example, given `differences = [1, -3, 4]`, `lower = 1`, `upper = 6`, the hidden sequence is a sequence of length `4` whose elements are in between `1` and `6` (**inclusive**).
Return *the number of ****possible**** hidden sequences there are.* If there are no possible sequences, return `0`.

**Example 1:**

```plain text
Input: differences = [1,-3,4], lower = 1, upper = 6
Output: 2
Explanation: The possible hidden sequences are:
- [3, 4, 1, 5]
- [4, 5, 2, 6]
Thus, we return 2.

```

**Example 2:**

```plain text
Input: differences = [3,-4,5,1,-2], lower = -4, upper = 5
Output: 4
Explanation: The possible hidden sequences are:
- [-3, 0, -4, 1, 2, 0]
- [-2, 1, -3, 2, 3, 1]
- [-1, 2, -2, 3, 4, 2]
- [0, 3, -1, 4, 5, 3]
Thus, we return 4.
```

**Example 3:**

```plain text
Input: differences = [4,-7,2], lower = 3, upper = 6
Output: 0
Explanation: There are no possible hidden sequences. Thus, we return 0.
```

**Constraints:**

- `n == differences.length`
- `1 <= n <= 105`
- `105 <= differences[i] <= 105`
- `105 <= lower <= upper <= 105`
```java
class Solution {
    public int numberOfArrays(int[] differences, int lower, int upper) {
        // 0 3 -1 4 5 3 
        long max = 0, min = 0;
        long init = 0;

        int len = differences.length;
        for(int i = 0; i < len; i++) {
            init += differences[i];
            max = Math.max(max, init);
            min = Math.min(min, init);
        }

        if(upper - lower < max - min)
            return 0;
        
        return (int)((upper - lower) - (max - min) + 1);
    }
}
```

