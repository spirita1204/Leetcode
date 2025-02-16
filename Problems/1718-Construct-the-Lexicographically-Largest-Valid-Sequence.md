# 1718. Construct the Lexicographically Largest Valid Sequence  

  Methods: DFS,Greedy </br> Difficulty: Medium </br> </br>Given an integer `n`, find a sequence that satisfies all of the following:

- The integer `1` occurs once in the sequence.
- Each integer between `2` and `n` occurs twice in the sequence.
- For every integer `i` between `2` and `n`, the **distance** between the two occurrences of `i` is exactly `i`.
The **distance** between two numbers on the sequence, `a[i]` and `a[j]`, is the absolute difference of their indices, `|j - i|`.

Return *the ****lexicographically largest**** sequence. It is guaranteed that under the given constraints, there is always a solution.*

A sequence `a` is lexicographically larger than a sequence `b` (of the same length) if in the first position where `a` and `b` differ, sequence `a` has a number greater than the corresponding number in `b`. For example, `[0,1,9,0]` is lexicographically larger than `[0,1,5,6]` because the first position they differ is at the third number, and `9` is greater than `5`.

**Example 1:**

```plain text
Input: n = 3
Output: [3,1,2,3,2]
Explanation: [2,3,2,1,3] is also a valid sequence, but [3,1,2,3,2] is the lexicographically largest valid sequence.

```

**Example 2:**

```plain text
Input: n = 5
Output: [5,3,1,4,3,5,2,4,2]

```

**Constraints:**

- `1 <= n <= 20`
```java
class Solution {
    public int[] constructDistancedSequence(int n) {
        int[] res = new int[n * 2 - 1]; // 初始化結果陣列，長度為 n * 2 - 1
        boolean[] visited = new boolean[n + 1]; // 用來標記 1 到 n 是否已經放置過

        calc(0, res, visited, n); // 從 index = 0 開始進行回溯

        return res;
    }

    private boolean calc(int index, int[] res, boolean[] visited, int n) {
        // 若已經放置到陣列末尾，表示成功找到一組符合條件的序列
        if (index == res.length) {
            return true;
        }

        // 若當前位置已被填入數字，則跳過，進入下一個 index
        if (res[index] != 0) {
            return calc(index + 1, res, visited, n);
        } else {
            // 從 n 開始遞減，確保字典序最大
            for (int i = n; i >= 1; i--) {
                if (visited[i]) continue; // 若 i 已經使用過則跳過

                visited[i] = true; // 標記 i 為已使用
                res[index] = i; // 放置 i 在當前 index 上

                if (i == 1) {
                    // 若 i 是 1，則只需放一次
                    if (calc(index + 1, res, visited, n)) 
                        return true;
                } else if (index + i < res.length && res[index + i] == 0) {
                    // 若 i > 1，則需放置兩次，且間隔為 i
                    res[index + i] = i;
                    if (calc(index + 1, res, visited, n)) 
                        return true;
                    // 若後續無法成功，則回溯
                    res[index + i] = 0;
                }

                // 回溯：重置目前已放置的數字與 visited 狀態
                res[index] = 0;
                visited[i] = false;
            }
        }
        return false;
    }
}

```

