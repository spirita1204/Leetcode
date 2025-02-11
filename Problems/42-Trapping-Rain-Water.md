# 42. Trapping Rain Water

Methods: Pointer
Difficulty: Hard

Hard

Topics

Companies

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9

```

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

## **Time Limit Exceeded**

```java
class Solution {
    public int trap(int[] height) {
        int sum = 0;

        while (isContain(height)) {
            sum += sum(height);
            sub(height);  
        }
        return sum;
    }

    private int sum(int[] height) {
        int sum = 0;
        int p1 = 0, p2 = 1;
        while (p2 < height.length) {
            while (p1 < height.length - 1) {
                if (height[p1] > 0 && height[p1 + 1] <= 0) break;
                else p1++;
            }
            p2 = p1 + 1;
            if(p2 == height.length - 1) break;
            while (p2 < height.length) {
                if (height[p2] > 0 && height[p2 - 1] <= 0) break;
                else p2++;
            }
            if(p2 == height.length) break;
            sum += (p2 - p1 - 1);//
            p1 = p2;
        }
        return sum;
    }

    private void sub(int[] height) {
        for (int i = 0; i < height.length; i++) {
            height[i] -= 1;
        }
    }

    private boolean isContain(int[] height) {
        for (int i : height) {
            if (i > 0)
                return true;
        }
        return false;
    }
}
```

```java
public class Solution {
    public int trap(int[] h) {
        // 每點是取左邊與右邊最大中最小
        int n = h.length;
        int[] leftMost = new int[n];
        int[] rightMost = new int[n];
        int sum = 0;

        for(int i = 1; i < n; i++) {
            leftMost[i] = Math.max(leftMost[i - 1], h[i - 1]);
        }
        for(int i = n - 2; i >= 0; i--) {
            rightMost[i] = Math.max(rightMost[i + 1], h[i + 1]);
        }
        for(int i = 1; i < n - 1; i++) {
            int val = Math.min(leftMost[i], rightMost[i]) - h[i];
            if(val > 0) sum += val;
        }
        return sum;
    }
}
```