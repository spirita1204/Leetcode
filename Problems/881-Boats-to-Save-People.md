# 881. Boats to Save People

Methods: Pointer
Difficulty: Easy

**Medium**

4.3K

110

Companies

You are given an array `people` where `people[i]` is the weight of the `ith` person, and an **infinite number of boats** where each boat can carry a maximum weight of `limit`. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most `limit`.

Return *the minimum number of boats to carry every given person*.

**Example 1:**

```
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)

```

**Example 2:**

```
Input: people = [3,2,2,1], limit = 3
Output: 3
Explanation: 3 boats (1, 2), (2) and (3)

```

**Example 3:**

```
Input: people = [3,5,3,4], limit = 5
Output: 4
Explanation: 4 boats (3), (3), (4), (5)

```

**Constraints:**

- `1 <= people.length <= 5 * 104`
- `1 <= people[i] <= limit <= 3 * 104`

```java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        Arrays.sort(people);
        int len = people.length;
        int p1 = 0, p2 = len - 1;
        int boat = 0;

        while(p1 < p2) {
            if(people[p2] + people[p1] > limit) {
                boat++;
                p2--;
            } else {
                boat++;
                p2--;
                p1++;
            }
        }
        if(p1 == p2) boat++;
        return boat;
    }
}
```