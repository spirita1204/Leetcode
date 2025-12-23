# 3433. Count Mentions Per User  

  Methods: Basic logic </br> Data Structure: Hash Table </br> Difficulty: Medium </br> </br>You are given an integer `numberOfUsers` representing the total number of users and an array `events` of size `n x 3`.

Each `events[i]` can be either of the following two types:

1. **Message Event:** `["MESSAGE", "timestampi", "mentions_stringi"]` 
1. **Offline Event:** `["OFFLINE", "timestampi", "idi"]`
Return an array `mentions` where `mentions[i]` represents the number of mentions the user with id `i` has across all `MESSAGE` events.

All users are initially online, and if a user goes offline or comes back online, their status change is processed *before* handling any message event that occurs at the same timestamp.

**Note **that a user can be mentioned **multiple** times in a **single** message event, and each mention should be counted **separately**.

**Example 1:  **

**Input:** numberOfUsers = 2, events = [["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","71","HERE"]]

**Output:** [2,2]

**Explanation:**

Initially, all users are online.

At timestamp 10, `id1` and `id0` are mentioned. `mentions = [1,1]`

At timestamp 11, `id0` goes **offline.**

At timestamp 71, `id0` comes back **online** and `"HERE"` is mentioned. `mentions = [2,2]`

**Example 2:**

**Input:** numberOfUsers = 2, events = [["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","12","ALL"]]

**Output:** [2,2]

**Explanation:**

Initially, all users are online.

At timestamp 10, `id1` and `id0` are mentioned. `mentions = [1,1]`

At timestamp 11, `id0` goes **offline.**

At timestamp 12, `"ALL"` is mentioned. This includes offline users, so both `id0` and `id1` are mentioned. `mentions = [2,2]`

**Example 3:**

**Input:** numberOfUsers = 2, events = [["OFFLINE","10","0"],["MESSAGE","12","HERE"]]

**Output:** [0,1]

**Explanation:**

Initially, all users are online.

At timestamp 10, `id0` goes **offline.**

At timestamp 12, `"HERE"` is mentioned. Because `id0` is still offline, they will not be mentioned. `mentions = [0,1]`

**Constraints:**

- `1 <= numberOfUsers <= 100`
- `1 <= events.length <= 100`
- `events[i].length == 3`
- `events[i][0]` will be one of `MESSAGE` or `OFFLINE`.
- `1 <= int(events[i][1]) <= 105`
- The number of `id<number>` mentions in any `"MESSAGE"` event is between `1` and `100`.
- `0 <= <number> <= numberOfUsers - 1`
- It is **guaranteed** that the user id referenced in the `OFFLINE` event is **online** at the time the event occurs.
```java
class Solution {
    public int[] countMentions(int numberOfUsers, List<List<String>> events) {
        TreeMap<Integer, List<List<String>>> byTime = new TreeMap<>();
        for (List<String> ev : events) {
            int t = Integer.parseInt(ev.get(1));
            byTime.computeIfAbsent(t, k -> new ArrayList<>()).add(ev);
        }

        int[] mentions = new int[numberOfUsers];
        boolean[] isOnline = new boolean[numberOfUsers];
        int[] offlineUntil = new int[numberOfUsers];
        Arrays.fill(isOnline, true);

        for (Map.Entry<Integer, List<List<String>>> entry : byTime.entrySet()) {
            int t = entry.getKey();
            List<List<String>> evs = entry.getValue();

            for (int i = 0; i < numberOfUsers; ++i) {
                if (!isOnline[i] && offlineUntil[i] <= t) {
                    isOnline[i] = true;
                    offlineUntil[i] = 0;
                }
            }

            for (List<String> ev : evs) {
                if (ev.get(0).equals("OFFLINE")) {
                    int id = Integer.parseInt(ev.get(2));
                    isOnline[id] = false;
                    offlineUntil[id] = t + 60;
                }
            }

            for (List<String> ev : evs) {
                if (!ev.get(0).equals("MESSAGE")) continue;
                String mentionsStr = ev.get(2);
                String[] tokens = mentionsStr.split("\\s+");
                for (String token : tokens) {
                    if (token.equals("ALL")) {
                        for (int i = 0; i < numberOfUsers; ++i) 
                            mentions[i]++;
                    } else if (token.equals("HERE")) {
                        for (int i = 0; i < numberOfUsers; ++i)
                            if (isOnline[i]) mentions[i]++;
                    } else if (token.startsWith("id")) {
                        int id = Integer.parseInt(token.substring(2));
                        if (id >= 0 && id < numberOfUsers) mentions[id]++;
                    }
                }
            }
        }

        return mentions;
    }
}
```

