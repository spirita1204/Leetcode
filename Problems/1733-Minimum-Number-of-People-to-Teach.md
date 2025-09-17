# 1733. Minimum Number of People to Teach  

  Methods: Basic logic </br> Difficulty: Medium </br> </br>On a social network consisting of `m` users and some friendships between users, two users can communicate with each other if they know a common language.

You are given an integer `n`, an array `languages`, and an array `friendships` where:

- There are `n` languages numbered `1` through `n`,
- `languages[i]` is the set of languages the `ith` user knows, and
- `friendships[i] = [ui, vi]` denotes a friendship between the users `ui` and `vi`.
You can choose **one** language and teach it to some users so that all friends can communicate with each other. Return *the* ***minimum**** number of users you need to teach.*

Note that friendships are not transitive, meaning if x is a friend of y and y is a friend of z , this doesn't guarantee that x is a friend of z .

**Example 1:**

```plain text
Input: n = 2, languages = [[1],[2],[1,2]], friendships = [[1,2],[1,3],[2,3]]
Output: 1
Explanation: You can either teach user 1 the second language or user 2 the first language.
```

**Example 2:**

```plain text
Input: n = 3, languages = [[2],[1,3],[1,2],[3]], friendships = [[1,4],[1,2],[3,4],[2,3]]
Output: 2
Explanation: Teach the third language to users 1 and 3, yielding two users to teach.
```

**Constraints:**

- `2 <= n <= 500`
- `languages.length == m`
- `1 <= m <= 500`
- `1 <= languages[i].length <= n`
- `1 <= languages[i][j] <= n`
- `1 <= ui < vi <= languages.length`
- `1 <= friendships.length <= 500`
- All tuples `(ui, vi)` are unique
- `languages[i]` contains only unique values
```java
class Solution {
    public int minimumTeachings(int n, int[][] languages, int[][] friendships) {
        Set<Integer> usersToTeach = new HashSet<>();
        
        // Step 1: Find users who cannot communicate
        for (int[] friendship : friendships) {
            int u1 = friendship[0] - 1;
            int u2 = friendship[1] - 1;
            boolean canCommunicate = false;
            
            for (int lang1 : languages[u1]) {
                for (int lang2 : languages[u2]) {
                    if (lang1 == lang2) {
                        canCommunicate = true;
                        break;
                    }
                }
                if (canCommunicate) break;
            }
            
            if (!canCommunicate) {
                usersToTeach.add(u1);
                usersToTeach.add(u2);
            }
        }
        
        int minUsersToTeach = languages.length + 1;
        
        // Step 2: Try each language
        for (int lang = 1; lang <= n; lang++) {
            int count = 0;
            
            for (int user : usersToTeach) {
                boolean knows = false;
                for (int l : languages[user]) {
                    if (l == lang) {
                        knows = true;
                        break;
                    }
                }
                if (!knows) count++;
            }
            
            minUsersToTeach = Math.min(minUsersToTeach, count);
        }
        
        return minUsersToTeach;
    }
}
```

