# 3170. Lexicographically Minimum String After Removing Stars

Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

You are given a string `s`. It may contain any number of `'*'` characters. Your task is to remove all `'*'` characters.

While there is a `'*'`, do the following operation:

- Delete the leftmost `'*'` and the **smallest** non-`'*'` character to its *left*. If there are several smallest characters, you can delete any of them.

Return the

lexicographically smallest

resulting string after removing all

```
'*'
```

characters.

**Example 1:**

```java
**Input:** s = "aaba*"

**Output:** "aab"
```

**Explanation:**

We should delete one of the `'a'` characters with `'*'`. If we choose `s[3]`, `s` becomes the lexicographically smallest.

**Example 2:**

```java
**Input:** s = "abc"

**Output:** "abc"
```

**Explanation:**

There is no `'*'` in the string.

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists only of lowercase English letters and `'*'`.
- The input is generated such that it is possible to delete all `'*'` characters.

跑時間有久

```java
**class Solution {
    public String clearStars(String s) {
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> s.charAt(a) == s.charAt(b) ? b - a : s.charAt(a) - s.charAt(b));
        StringBuilder sb = new StringBuilder(s);
        
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c == '*' && !pq.isEmpty()) {
                // sb.deleteCharAt(pq.poll()); 
                // tip 將該點替換成* 最後統一刪
                int delI = pq.poll();
                sb.replace(delI, delI + 1, "*");
            } else {
                pq.offer(i);
            } 
        }
        return sb.toString().replace("*", "");
    }
}**
```

優化一點

```java
class Solution {
    public String clearStars(String s) {
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> s.charAt(a) == s.charAt(b) ? b - a : s.charAt(a) - s.charAt(b));
        StringBuilder sb = new StringBuilder();
        Set<Integer> hs = new HashSet<>();

        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c == '*' && !pq.isEmpty()) {
                hs.add(pq.poll());
            } else {
                pq.offer(i);
            } 
        }
        // 透過蒐集欲刪除的index set 統一刪除
        for(int i = 0; i < s.length(); i++) {
            if(!hs.contains(i) && s.charAt(i) != '*') 
                sb.append(s.charAt(i));
        }
        return sb.toString();
    }
}
```

![Untitled](Untitled%2018.png)