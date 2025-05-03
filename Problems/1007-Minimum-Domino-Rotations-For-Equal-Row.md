# 1007. Minimum Domino Rotations For Equal Row  

  Methods: Array </br> Difficulty: Medium </br> </br>In a row of dominoes, `tops[i]` and `bottoms[i]` represent the top and bottom halves of the `ith` domino. (A domino is a tile with two numbers from 1 to 6 - one on each half of the tile.)

We may rotate the `ith` domino, so that `tops[i]` and `bottoms[i]` swap values. 

Return the minimum number of rotations so that all the values in `tops` are the same, or all the values in `bottoms` are the same.

If it cannot be done, return `-1`.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/05/14/domino.png)

```plain text
Input: tops = [2,1,2,4,2,2], bottoms = [5,2,6,2,3,2]
Output: 2
Explanation:
The first figure represents the dominoes as given by tops and bottoms: before we do any rotations.
If we rotate the second and fourth dominoes, we can make every value in the top row equal to 2, as indicated by the second figure.
```

**Example 2:**

```plain text
Input: tops = [3,5,1,2,3], bottoms = [3,6,3,3,4]
Output: -1
Explanation:
In this case, it is not possible to rotate the dominoes to make one row of values equal.
```

**Constraints:**

- `2 <= tops.length <= 2 * 104`
- `bottoms.length == tops.length`
- `1 <= tops[i], bottoms[i] <= 6`
```java
class Solution {
    public int minDominoRotations(int[] tops, int[] bottoms) {
        // 只需考慮tops[0] bottoms[0]
        int result = check(tops[0], tops, bottoms);
        if (result != -1)
            return result;

        return check(bottoms[0], tops, bottoms);
    }

    private int check(int target, int[] tops, int[] bottoms) {
        int topRotations = 0;
        int bottomRotations = 0;

        for (int i = 0; i < tops.length; i++) {
            if (tops[i] != target && bottoms[i] != target) 
                return -1; // 無法讓第 i 張骨牌有目標值
            else if (tops[i] != target) 
                topRotations++; // 需要把 bottoms[i] 移到 tops[i]
            else if (bottoms[i] != target) 
                bottomRotations++; // 需要把 tops[i] 移到 bottoms[i]
        }

        return Math.min(topRotations, bottomRotations);
    }
}

```

