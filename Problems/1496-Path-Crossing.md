# 1496. Path Crossing

Methods: Basic logic
Data structure: Set
Difficulty: Easy

Easy

Topics

Companies

Hint

Given a string `path`, where `path[i] = 'N'`, `'S'`, `'E'` or `'W'`, each representing moving one unit north, south, east, or west, respectively. You start at the origin `(0, 0)` on a 2D plane and walk on the path specified by `path`.

Return `true` *if the path crosses itself at any point, that is, if at any time you are on a location you have previously visited*. Return `false` otherwise.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/06/10/screen-shot-2020-06-10-at-123929-pm.png](https://assets.leetcode.com/uploads/2020/06/10/screen-shot-2020-06-10-at-123929-pm.png)

```
Input: path = "NES"
Output: false
Explanation: Notice that the path doesn't cross any point more than once.

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/06/10/screen-shot-2020-06-10-at-123843-pm.png](https://assets.leetcode.com/uploads/2020/06/10/screen-shot-2020-06-10-at-123843-pm.png)

```
Input: path = "NESWW"
Output: true
Explanation: Notice that the path visits the origin twice.
```

**Constraints:**

- `1 <= path.length <= 104`
- `path[i]` is either `'N'`, `'S'`, `'E'`, or `'W'`.

---

Seen this question in a real interview before?

**1/4**

Yes

No

Accepted

**108.2K**

Submissions

**177.4K**

Acceptance Rate

**61.0%**

---

```java
class Solution {
    public boolean isPathCrossing(String path) {
        Set<String> s = new HashSet<>();
        s.add("0,0");
        int x = 0, y = 0;
        
        for(int i = 0; i< path.length(); i++) {
            char c = path.charAt(i);
            
            switch(c) {
                case 'N': // 上
                    y++;
                    break;
                case 'S': // 南 
                    y--;
                    break;
                case 'E': // 東
                    x++; 
                    break;
                case 'W': // 西 
                    x--;
                    break;
            }
            boolean addSuccess = s.add(String.valueOf(x)+','+String.valueOf(y));
            if(!addSuccess) return true;
        }
        return false;
    }
}
```