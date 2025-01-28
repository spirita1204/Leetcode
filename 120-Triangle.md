# 120. Triangle

Methods: DP
Difficulty: Medium

**Medium**

7.8K

466

Given a `triangle` array, return *the minimum path sum from top to bottom*.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

```
Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11
Explanation: The triangle looks like:
23 4
 65 7
41 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).

```

**Example 2:**

```
Input: triangle = [[-10]]
Output: -10

```

**Constraints:**

- `1 <= triangle.length <= 200`
- `triangle[0].length == 1`
- `triangle[i].length == triangle[i - 1].length + 1`
- `104 <= triangle[i][j] <= 104`

**Follow up:**

Could you do this using only

```
O(n)
```

extra space, where

```
n
```

is the total number of rows in the triangle?

TLE  DFS

```jsx
class Solution {
    int min = Integer.MAX_VALUE;
    int depth = 0;
    public int minimumTotal(List<List<Integer>> triangle) {
        depth = triangle.size() - 1;
        recursion(triangle, 0, triangle.get(0).get(0), 0);
        return min;
    }
    public void recursion(List<List<Integer>> triangle, int nowDepth, int total, int index){
        if(nowDepth + 1> depth){
            min = Math.min(min, total);
            return;
        }

        int left = triangle.get(nowDepth +1).get(index);
        int right = triangle.get(nowDepth + 1).get(index+1);

        recursion(triangle, nowDepth + 1, total + left, index);
        recursion(triangle, nowDepth + 1, total + right, index + 1);
    }
}
```

DP BEST SOLUTION

```jsx
// USE DP
    public int minimumTotal(List<List<Integer>> triangle) {
        int[] dp = new int[triangle.size() + 1]; 

        for(int i = triangle.size() - 1; i >= 0; i--){
            for(int j = 0; j < triangle.get(i).size(); j++){
                dp[j] = Math.min(dp[j], dp[j + 1]) + triangle.get(i).get(j);
            }
        }
        return dp[0];
    }
```