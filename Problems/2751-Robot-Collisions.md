# 2751. Robot Collisions

Data structure: Stack
Difficulty: Hard

Hard

Topics

Companies

Hint

There are `n` **1-indexed** robots, each having a position on a line, health, and movement direction.

You are given **0-indexed** integer arrays `positions`, `healths`, and a string `directions` (`directions[i]` is either **'L'** for **left** or **'R'** for **right**). All integers in `positions` are **unique**.

All robots start moving on the line **simultaneously** at the **same speed** in their given directions. If two robots ever share the same position while moving, they will **collide**.

If two robots collide, the robot with **lower health** is **removed** from the line, and the health of the other robot **decreases** **by one**. The surviving robot continues in the **same** direction it was going. If both robots have the **same** health, they are both ****removed from the line.

Your task is to determine the **health** of the robots that survive the collisions, in the same **order** that the robots were given, ****i.e. final heath of robot 1 (if survived), final health of robot 2 (if survived), and so on. If there are no survivors, return an empty array.

Return *an array containing the health of the remaining robots (in the order they were given in the input), after no further collisions can occur.*

**Note:** The positions may be unsorted.

**Example 1:**

![https://assets.leetcode.com/uploads/2023/05/15/image-20230516011718-12.png](https://assets.leetcode.com/uploads/2023/05/15/image-20230516011718-12.png)

```
Input: positions = [5,4,3,2,1], healths = [2,17,9,15,10], directions = "RRRRR"
Output: [2,17,9,15,10]
Explanation: No collision occurs in this example, since all robots are moving in the same direction. So, the health of the robots in order from the first robot is returned, [2, 17, 9, 15, 10].

```

**Example 2:**

![https://assets.leetcode.com/uploads/2023/05/15/image-20230516004433-7.png](https://assets.leetcode.com/uploads/2023/05/15/image-20230516004433-7.png)

```
Input: positions = [3,5,2,6], healths = [10,10,15,12], directions = "RLRL"
Output: [14]
Explanation: There are 2 collisions in this example. Firstly, robot 1 and robot 2 will collide, and since both have the same health, they will be removed from the line. Next, robot 3 and robot 4 will collide and since robot 4's health is smaller, it gets removed, and robot 3's health becomes 15 - 1 = 14. Only robot 3 remains, so we return [14].

```

**Example 3:**

![https://assets.leetcode.com/uploads/2023/05/15/image-20230516005114-9.png](https://assets.leetcode.com/uploads/2023/05/15/image-20230516005114-9.png)

```
Input: positions = [1,2,5,6], healths = [10,10,11,11], directions = "RLRL"
Output: []
Explanation: Robot 1 and robot 2 will collide and since both have the same health, they are both removed. Robot 3 and 4 will collide and since both have the same health, they are both removed. So, we return an empty array, [].
```

**Constraints:**

- `1 <= positions.length == healths.length == directions.length == n <= 105`
- `1 <= positions[i], healths[i] <= 109`
- `directions[i] == 'L'` or `directions[i] == 'R'`
- All values in `positions` are distinct

```java
class Solution {
    public List<Integer> survivedRobotsHealths(int[] positions, int[] healths, String directions) {
        List<int[]> res = new ArrayList<>();
        Stack<int[]> st = new Stack<>();
        int length = positions.length;
        int[][] sortByPosition = new int[length][4];
        for (int i = 0; i < length; i++) {
            sortByPosition[i][0] = positions[i];
            sortByPosition[i][1] = healths[i];
            sortByPosition[i][2] = (directions.substring(i, i + 1).equals("L")) ? -1 : 1;
            sortByPosition[i][3] = i;// 固定原來排序
        }
        Arrays.sort(sortByPosition, (a, b) -> a[0] - b[0]);

        for (int i = 0; i < length; i++) {
            // 不會相撞 往左
            if (st.isEmpty() && sortByPosition[i][2] == -1)
                res.add(sortByPosition[i]);
            else {
                if (sortByPosition[i][2] == 1)
                    st.push(sortByPosition[i]);
                else {// -> <-
                    while(!st.isEmpty()) {
                        int[] e = st.pop();// 左
                        if (e[1] < sortByPosition[i][1]) {// 右大
                            sortByPosition[i][1]--;// health--
                            // 當大於一切 則加到輸出
                            if(st.isEmpty()) res.add(sortByPosition[i]);
                        } else if (e[1] > sortByPosition[i][1]) {// 左大
                            e[1]--;// health--
                            st.push(e);
                            break;
                        } else {// 相等
                            // 一起collision
                            break;
                        }
                    }
                }
            }
        }
        while (!st.isEmpty())
            res.add(st.pop());
        // 確保排序和原本一樣
        Collections.sort(res, (a, b) -> a[3] - b[3]);
        List<Integer> sortRes = new ArrayList<>();
        
        for(int[] i: res) {
            sortRes.add(i[1]);
        }
        return sortRes;
    }
}

// 5 12 46
// 3 43 27
// r  l  l

// 11 16 44
// 1  17 20
// r  r  l
```