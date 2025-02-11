# 84. Largest Rectangle in Histogram

Data structure: Stack
Difficulty: Hard

Hard

Topics

Companies

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

```
Input: heights = [2,4]
Output: 4

```

**Constraints:**

- `1 <= heights.length <= 105`
- `0 <= heights[i] <= 104`

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        // 找以當前為高 小於當前高的左邊idx 右邊idx 相乘
        // max(area[i] = height[i]* (nextSmaller[i] - preSmaller[i] - 1))
        Stack<Integer> st = new Stack<>();
        int len = heights.length;
        int[] preSmaller = new int[len];
        int[] nextSmaller = new int[len];
        Arrays.fill(preSmaller, -1);
        Arrays.fill(nextSmaller, len);
        int max = 0;

        // 右邊小於當前
        for(int i = 0; i < len; i++) {
            int h = heights[i];
            while(!st.isEmpty() && heights[st.peek()] > h ) {
                nextSmaller[st.pop()] = i;
            }
            st.push(i);
        }
        // 左邊小於當前
        for(int i = len - 1; i >= 0; i--) {
            int h = heights[i];
            while(!st.isEmpty() && heights[st.peek()] > h ) {
                preSmaller[st.pop()] = i;
            }
            st.push(i);
        }
        // 計算最大面積
        for(int i = 0; i< len; i++) {
            max = Math.max(max, (nextSmaller[i] - preSmaller[i] - 1)* heights[i]);
        }
        return max;
    }
}
```