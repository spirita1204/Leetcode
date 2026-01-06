# 1975. Maximum Matrix Sum  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>You are given an `n x n` integer `matrix`. You can do the following operation **any** number of times:

- Choose any two **adjacent** elements of `matrix` and **multiply** each of them by `1`.
Two elements are considered **adjacent** if and only if they share a **border**.

Your goal is to **maximize** the summation of the matrix's elements. Return *the ****maximum**** sum of the matrix's elements using the operation mentioned above.*

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/07/16/pc79-q2ex1.png)

```plain text
Input: matrix = [[1,-1],[-1,1]]
Output: 4  
Explanation: We can follow the following steps to reach sum equals 4:
- Multiply the 2 elements in the first row by -1.
- Multiply the 2 elements in the first column by -1.
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/07/16/pc79-q2ex2.png)

```plain text
Input: matrix = [[1,2,3],[-1,-2,-3],[1,2,3]]
Output: 16
Explanation: We can follow the following step to reach sum equals 16:
- Multiply the 2 last elements in the second row by -1.
```

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `2 <= n <= 250`
- `105 <= matrix[i][j] <= 105`
```java
class Solution {
    public long maxMatrixSum(int[][] matrix) {
        // 負數個數是奇數」時，一定要留下 1 個最小絕對值的負數
        int min = Integer.MAX_VALUE;
        long sum = 0;
        int negCount = 0;
        for (int i = 0; i < matrix.length; i++)
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] < 0)
                    negCount++;
                int ab = Math.abs(matrix[i][j]);
                min = Math.min(min, ab);
                sum += ab;
            }
        if (negCount % 2 == 0)
            return sum;
        return sum - 2 * min;
    }
}
```

