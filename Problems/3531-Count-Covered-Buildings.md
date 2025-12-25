# 3531. Count Covered Buildings  

  Data Structure: TreeSet,Hash Table </br> Difficulty: Medium </br> </br>You are given a positive integer `n`, representing an `n x n` city. You are also given a 2D grid `buildings`, where `buildings[i] = [x, y]` denotes a **unique** building located at coordinates `[x, y]`.

A building is **covered** if there is at least one building in all **four** directions: left, right, above, and below.

Return the number of **covered** buildings.

**Example 1:**

![Image](https://assets.leetcode.com/uploads/2025/03/04/telegram-cloud-photo-size-5-6212982906394101085-m.jpg)

**Input:** n = 3, buildings = [[1,2],[2,2],[3,2],[2,1],[2,3]]

**Output:** 1

**Explanation:**

- Only building `[2,2]` is covered as it has at least one building:
- Thus, the count of covered buildings is 1.
**Example 2:**

![Image](https://assets.leetcode.com/uploads/2025/03/04/telegram-cloud-photo-size-5-6212982906394101086-m.jpg)

**Input:** n = 3, buildings = [[1,1],[1,2],[2,1],[2,2]]

**Output:** 0

**Explanation:**

- No building has at least one building in all four directions.
**Example 3:**

![Image](https://assets.leetcode.com/uploads/2025/03/16/telegram-cloud-photo-size-5-6248862251436067566-x.jpg)

**Input:** n = 5, buildings = [[1,3],[3,2],[3,3],[3,5],[5,3]]

**Output:** 1

**Explanation:  **

- Only building `[3,3]` is covered as it has at least one building:
- Thus, the count of covered buildings is 1.
**Constraints:**

- `2 <= n <= 105`
- `1 <= buildings.length <= 105`
- `buildings[i] = [x, y]`
- `1 <= x, y <= n`
- All coordinates of `buildings` are **unique**.
```java
class Solution {
    public int countCoveredBuildings(int n, int[][] buildings) {
        Map<Integer, TreeSet<Integer>> rowToCol = new HashMap<>();
        Map<Integer, TreeSet<Integer>> colToRow = new HashMap<>();
        for (int building[] : buildings) {
            int x = building[0], y = building[1];
            rowToCol.computeIfAbsent(x, k -> new TreeSet<>()).add(y);
            colToRow.computeIfAbsent(y, k -> new TreeSet<>()).add(x);
        }
        int cnt = 0;
        for (int building[] : buildings) {
            int x = building[0], y = building[1];
            
            TreeSet<Integer> cols = rowToCol.get(x);
            TreeSet<Integer> rows = colToRow.get(y);
            
            Integer left = cols.lower(y);
            Integer right = cols.higher(y);
            Integer up = rows.lower(x);
            Integer down = rows.higher(x);
            
            if ((left != null) && (right != null) && (up != null) && (down != null)) {
                cnt++;
            }
        }
        return cnt;
    }
}
```

