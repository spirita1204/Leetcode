# 2069. Walking Robot Simulation II  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>A `width x height` grid is on an XY-plane with the **bottom-left** cell at `(0, 0)` and the **top-right** cell at `(width - 1, height - 1)`. The grid is aligned with the four cardinal directions (`"North"`, `"East"`, `"South"`, and `"West"`). A robot is **initially** at cell `(0, 0)` facing direction `"East"`.

The robot can be instructed to move for a specific number of **steps**. For each step, it does the following.   

1. Attempts to move **forward one** cell in the direction it is facing.
1. If the cell the robot is **moving to** is **out of bounds**, the robot instead **turns** 90 degrees **counterclockwise** and retries the step.
After the robot finishes moving the number of steps required, it stops and awaits the next instruction.

Implement the `Robot` class:

- `Robot(int width, int height)` Initializes the `width x height` grid with the robot at `(0, 0)` facing `"East"`.
- `void step(int num)` Instructs the robot to move forward `num` steps.
- `int[] getPos()` Returns the current cell the robot is at, as an array of length 2, `[x, y]`.
- `String getDir()` Returns the current direction of the robot, `"North"`, `"East"`, `"South"`, or `"West"`.
**Example 1:**

![Image](https://assets.leetcode.com/uploads/2021/10/09/example-1.png)

```plain text
Input
["Robot", "step", "step", "getPos", "getDir", "step", "step", "step", "getPos", "getDir"]
[[6, 3], [2], [2], [], [], [2], [1], [4], [], []]
Output
[null, null, null, [4, 0], "East", null, null, null, [1, 2], "West"]

Explanation  
Robot robot = new Robot(6, 3); // Initialize the grid and the robot at (0, 0) facing East.
robot.step(2);  // It moves two steps East to (2, 0), and faces East.
robot.step(2);  // It moves two steps East to (4, 0), and faces East.
robot.getPos(); // return [4, 0]
robot.getDir(); // return "East"
robot.step(2);  // It moves one step East to (5, 0), and faces East.
                // Moving the next step East would be out of bounds, so it turns and faces North.
                // Then, it moves one step North to (5, 1), and faces North.
robot.step(1);  // It moves one step North to (5, 2), and faces North (not West).
robot.step(4);  // Moving the next step North would be out of bounds, so it turns and faces West.
                // Then, it moves four steps West to (1, 2), and faces West.
robot.getPos(); // return [1, 2]
robot.getDir(); // return "West"
```

**Constraints:**

- `2 <= width, height <= 100`
- `1 <= num <= 105`
- At most `104` calls **in total** will be made to `step`, `getPos`, and `getDir`.
```javascript
class Robot {
    int x, y, width, height;
    String dir;

    public Robot(int width, int height) {
        this.x = 0;
        this.y = 0;
        this.dir = "East";
        this.width = width;
        this.height = height;
    }

    public void step(int num) {
        int perim = 2 * (width - 1) + 2 * (height - 1); // 计算网格的周长
        num %= perim; // 将步数限制在周长内
        if (num == 0)
            num = perim; // 如果步数是周长的倍数，则设置为周长

        while (num > 0) {
            if (dir.equals("East")) { // 如果机器人面向东方
                int maxX = Math.min(x + num, width - 1); // 计算可以向东移动的最大距离，不超过网格边界
                int rem = num - (maxX - x); // 计算超出边界的步数
                num = rem; // 更新剩余步数
                if (rem == 0) // 如果没有超出边界
                    x = maxX; // 直接更新 x 坐标
                else { // 如果超出边界
                    x = maxX; // 移动到边界
                    dir = "North"; // 转向北方
                }
            } else if (dir.equals("West")) { // 如果机器人面向西方
                int minX = Math.max(x - num, 0);
                int rem = num - (x - minX);
                num = rem;
                if (rem == 0)
                    x = minX;
                else {
                    x = minX;
                    dir = "South";
                }
            } else if (dir.equals("North")) { // 如果机器人面向北方
                int maxY = Math.min(y + num, height - 1);
                int rem = num - (maxY - y);
                num = rem;
                if (rem == 0)
                    y = maxY;
                else {
                    y = maxY;
                    dir = "West";
                }
            } else if (dir.equals("South")) { // 如果机器人面向南方
                int minY = Math.max(y - num, 0);
                int rem = num - (y - minY);
                num = rem;
                if (rem == 0)
                    y = minY;
                else {
                    y = minY;
                    dir = "East";
                }
            }
        }
    }

    public int[] getPos() {
        return new int[] { x, y };
    }

    public String getDir() {
        return dir;
    }
}
```

