# 1405. Longest Happy String

Methods: Greedy
Data structure: Heap
Difficulty: Medium++

A string `s` is called **happy** if it satisfies the following conditions:

- `s` only contains the letters `'a'`, `'b'`, and `'c'`.
- `s` does not contain any of `"aaa"`, `"bbb"`, or `"ccc"` as a substring.
- `s` contains **at most** `a` occurrences of the letter `'a'`.
- `s` contains **at most** `b` occurrences of the letter `'b'`.
- `s` contains **at most** `c` occurrences of the letter `'c'`.

Given three integers `a`, `b`, and `c`, return *the **longest possible happy** string*. If there are multiple longest happy strings, return *any of them*. If there is no such string, return *the empty string* `""`.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

```
Input: a = 1, b = 1, c = 7
Output: "ccaccbcc"
Explanation: "ccbccacc" would also be a correct answer.

```

**Example 2:**

```
Input: a = 7, b = 1, c = 0
Output: "aabaa"
Explanation: It is the only correct answer in this case.

```

**Constraints:**

- `0 <= a, b, c <= 100`
- `a + b + c > 0`

```java
class Solution {
    public String longestDiverseString(int a, int b, int c) {
        StringBuilder sb = new StringBuilder();
        Queue<Pair> pq = new PriorityQueue<>((aa, bb) -> bb.times - aa.times);
        if (a != 0)
            pq.offer(new Pair('a', a));
        if (b != 0)
            pq.offer(new Pair('b', b));
        if (c != 0)
            pq.offer(new Pair('c', c));

        while (!pq.isEmpty()) {
            Pair first = pq.poll();
            // Check if the last two characters in the result are the same as the current
            // character
            int len = sb.length();
            if (len >= 2 && sb.charAt(len - 1) == first.c && sb.charAt(len - 2) == first.c) {
                // If we can't use the character, try the next one
                if (pq.isEmpty()) {
                    // If there's no other character available, return the result so far
                    break;
                }
                Pair second = pq.poll();
                sb.append(second.c);
                second.times--;
                // Put the second character back if it still has remaining count
                if (second.times > 0) {
                    pq.offer(second);
                }
                // Put the first character back since we couldn't use it this time
                pq.offer(first);
            } else {
                // Add the character
                sb.append(first.c);
                first.times--;
                // Reinsert the character if it still has remaining count
                if (first.times > 0) {
                    pq.offer(first);
                }
            }
        }
        return sb.toString();
    }
}

class Pair {
    char c;
    int times;

    Pair(char c, int times) {
        this.c = c;
        this.times = times;
    }
}
```