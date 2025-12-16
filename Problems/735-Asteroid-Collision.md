# 735. Asteroid Collision  

  Data Structure: Stack </br> Difficulty: Medium </br> </br>Medium

Topics

Companies

Hint

We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

```plain text
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

```

**Example 2:**

```plain text
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.

```

**Example 3:**

```plain text
Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

```

**Constraints:**

- `2 <= asteroids.length <= 104`
- `1000 <= asteroids[i] <= 1000`
- `asteroids[i] != 0`
```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        st.push(asteroids[0]);

        for (int i = 1; i < asteroids.length; i++) {
            int size = st.size();
            if(size == 0)  st.push(asteroids[i]);
            while (size-- > 0) {
                int top = st.peek();
                if ((top > 0 && asteroids[i] < 0) || (top < 0 && asteroids[i] > 0)) {// 方向相反
                    if (Math.abs(top) < Math.abs(asteroids[i])) {
                        if (asteroids[i] < top)
                            st.pop();
                        if (size == 0)
                            st.push(asteroids[i]);
                    } else if (Math.abs(top) == Math.abs(asteroids[i])) {// 等於
                        if (asteroids[i] > top)
                            st.push(asteroids[i]);
                        else
                            st.pop();
                        break;
                    } else {
                        if (asteroids[i] > top)
                            st.push(asteroids[i]);
                        break;
                    }
                } else {
                    st.push(asteroids[i]);
                    break;
                }
            }
        }
        int[] res = new int[st.size()];
        int i = st.size() - 1;
        while (!st.isEmpty()) {
            res[i--] = st.pop();
        }
        return res;
    }
}
```

