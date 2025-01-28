# 2182. Construct String With Repeat Limit

Data structure: Heap
Difficulty: Medium

You are given a string `s` and an integer `repeatLimit`. Construct a new string `repeatLimitedString` using the characters of `s` such that no letter appears **more than** `repeatLimit` times **in a row**. You do **not** have to use all characters from `s`.

Return *the **lexicographically largest*** `repeatLimitedString` *possible*.

A string `a` is **lexicographically larger** than a string `b` if in the first position where `a` and `b` differ, string `a` has a letter that appears later in the alphabet than the corresponding letter in `b`. If the first `min(a.length, b.length)` characters do not differ, then the longer string is the lexicographically larger one.

**Example 1:**

```
Input: s = "cczazcc", repeatLimit = 3
Output: "zzcccac"
Explanation: We use all of the characters from s to construct the repeatLimitedString "zzcccac".
The letter 'a' appears at most 1 time in a row.
The letter 'c' appears at most 3 times in a row.
The letter 'z' appears at most 2 times in a row.
Hence, no letter appears more than repeatLimit times in a row and the string is a valid repeatLimitedString.
The string is the lexicographically largest repeatLimitedString possible so we return "zzcccac".
Note that the string "zzcccca" is lexicographically larger but the letter 'c' appears more than 3 times in a row, so it is not a valid repeatLimitedString.

```

**Example 2:**

```
Input: s = "aababab", repeatLimit = 2
Output: "bbabaa"
Explanation: We use only some of the characters from s to construct the repeatLimitedString "bbabaa".
The letter 'a' appears at most 2 times in a row.
The letter 'b' appears at most 2 times in a row.
Hence, no letter appears more than repeatLimit times in a row and the string is a valid repeatLimitedString.
The string is the lexicographically largest repeatLimitedString possible so we return "bbabaa".
Note that the string "bbabaaa" is lexicographically larger but the letter 'a' appears more than 2 times in a row, so it is not a valid repeatLimitedString.

```

**Constraints:**

- `1 <= repeatLimit <= s.length <= 105`
- `s` consists of lowercase English letters.

## **Time Limit Exceeded**

```java
class Solution {
    public String repeatLimitedString(String s, int repeatLimit) {
        Queue<Character> pq = new PriorityQueue<>(Collections.reverseOrder());
        StringBuilder sb = new StringBuilder();
        Stack<Character> st = new Stack<>();

        for(int i = 0; i < s.length(); i++) 
            pq.offer(s.charAt(i));
        int cnt = 0;
        char pre = ' ';
        while(pq.size() > 0) {
            char c = pq.poll();
            if(c == pre && cnt >= repeatLimit) {// 不能再塞
                cnt = 1;
                st.push(c);
                while(pq.size() > 0 && c == pq.peek()) {
                    pq.poll();
                    st.push(c);
                } 
                if(pq.size() == 0)
                    return sb.toString();
                char diff = pq.poll();
                sb.append(diff); 
                pre = diff;
                while(st.size() > 0) {
                    pq.offer(st.pop());
                }
            } else if(c == pre){
                cnt++;
                sb.append(c);
            } else {// 不同字母直接塞
                cnt = 1;
                sb.append(c);
                pre = c;
            }
        }
        return sb.toString();
    }
}
```

---

## Pass

```sql
class Solution {
    public String repeatLimitedString(String s, int repeatLimit) {
        // Count frequency of each character
        int[] freq = new int[26];
        for (char c : s.toCharArray())
            freq[c - 'a']++;
        // Use a max heap to order characters by frequency and lexicographical order
        PriorityQueue<Character> pq = new PriorityQueue<>((a, b) -> b - a);
        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0) {
                pq.offer((char) (i + 'a'));
            }
        }
        StringBuilder sb = new StringBuilder();
        while (!pq.isEmpty()) {
            char current = pq.poll();
            int count = Math.min(freq[current - 'a'], repeatLimit);
            // Append the allowed number of the current character
            for (int i = 0; i < count; i++) {
                sb.append(current);
            }
            freq[current - 'a'] -= count;
            // If there are still occurrences left, we need to insert a different character
            if (freq[current - 'a'] > 0) {
                if (pq.isEmpty()) {
                    // No other character to insert, break out
                    break;
                }
                // Insert the next most frequent character
                char next = pq.poll();
                sb.append(next);
                freq[next - 'a']--;
                // Reinsert the next character if there are occurrences left
                if (freq[next - 'a'] > 0) {
                    pq.offer(next);
                }
                // Reinsert the current character for future use
                pq.offer(current);
            }
        }
        return sb.toString();
    }
}
```