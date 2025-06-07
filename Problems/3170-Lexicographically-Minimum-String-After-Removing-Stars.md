# 3170. Lexicographically Minimum String After Removing Stars  

  Data Structure: Heap </br> Difficulty: Medium </br> </br>You are given a string `s`. It may contain any number of `'*'` characters. Your task is to remove all `'*'` characters.

While there is a `'*'`, do the following operation:

- Delete the leftmost `'*'` and the **smallest** non-`'*'` character to its *left*. If there are several smallest characters, you can delete any of them.
Return the lexicographically smallest resulting string after removing all '*' characters.

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
        ****Queue<Integer> pq = new PriorityQueue<>((a, b) -> s.charAt(a) == s.charAt(b) ? b - a : s.charAt(a) - s.charAt(b));****
        StringBuilder sb = new StringBuilder(s);
        
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c == '*' && !pq.isEmpty()) {
                // sb.deleteCharAt(pq.poll()); 
                // tip 將該點替換成* 最後統一刪
                int delI = pq.poll();
                ****sb.replace(delI, delI + 1, "*");****
            } else {
                pq.offer(i);
            } 
        }
        return sb.toString()****.replace("*", "");****
    }
}**
```

優化一點

```java
class Solution {
    public String clearStars(String s) {
        Queue<Integer> pq = new PriorityQueue<>(
                (a, b) -> s.charAt(a) == s.charAt(b) ? b - a : s.charAt(a) - s.charAt(b));
        StringBuilder sb = new StringBuilder();
        Set<Integer> hs = new HashSet<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '*' && !pq.isEmpty()) 
                hs.add(pq.poll());
            else 
                pq.offer(i);
        }
        // 透過蒐集欲刪除的index set 統一刪除
        for (int i = 0; i < s.length(); i++) {
            if (!hs.contains(i) && s.charAt(i) != '*')
                sb.append(s.charAt(i));
        }
        return sb.toString();
    }
}
```

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/257c3c94-b229-4eaa-872c-b2d6343910d8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QEWTG3C6%2F20250607%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250607T034512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIE0alzdQKNbCyedXVFz6HmbVpj50DBDIYzSl%2Fg6PBpHEAiAkYkSoZp2TOP%2Bf6cN2TlWcBUzWCwv0cHqGrvgOR%2Fbn7ir%2FAwhrEAAaDDYzNzQyMzE4MzgwNSIMMoXqc9TU8nDAX%2FaKKtwDK%2FEC%2FIl%2FYAn1Tn4pqIO7CSMYkeVB7D22uc773GjOBQq0klqfZKXjoBFDHP8DnP0pvmJ%2BxT43erJpa%2B8xMsx1VeX6xYQgRlHKR2nYLiKo6K2zUp9xR9hqC06JbGF%2B5pEA98lA%2FX%2B%2BO%2BHCFI49iNaK8Hls8m2HqUF2N8KvTQoVS3t19EkLj1tXnKMS9FG7yX7FjX07XFW6Z5JxsD87h%2BPKVzi5KdJM6jXKhv%2B5%2FCNiA5LfqMRMzcPcqmyjRInlzk%2FyNfFJC22ExSxldUAjgbD81Pu2vO1ocdKtMJy6sVyL9B8ZrazMvx5G5I0Ws9kfbG9OwwHIuEarQ6SdqBsIPLxYG8bb96t4tYFHbOS20uwnjUXs7yqSTV8YBJ8NULJ9MhEiOeAvgQwX0QYM5m%2FXaDLmHsMxXgp%2FBnrxwKxCCjyLYWufDMVLIf0ty59UyZrfBPGo6r8LSceFKc7GK263o8BjdKBIn6uC9PD8651zqWXUb2PzxAiUZJu4jPSPs9Eh83YjSYTJM%2F78Tx8raa5lzebDLcxUICiov3hDJpomewk1tbHCpZGNyXrkYWDXJvM%2Fi9HeMuB%2BE5%2FQtLU3w2GfKqZFlJ4lDQWffINUvd8wEPCFv5EtmBW3shx0jiIoXfww%2B8COwgY6pgEzw7CH8rislL8KUPw8J%2F%2FDLe8MqaExOIaq2erdkWz2KeHJs6LG9HIAkZxOmNhlM7%2FfIn265Qu1F0OwU%2BO203TPiYe4EygLf63Emk3VRCkhyskOamt7so7nK2crraXfPItsHUFmtSUEMCTETPvWe9bjmwcFr9nSklvEydAwZmWPxZrAq1sBLceu999XSwKj%2FV3DAVzzrEyN00KTlgVzu0T7YEwT5Nng&X-Amz-Signature=61ff3514a898a7f4c9aafc44c1d81067370f8bacf29b7622345eaf151e4a44f5&X-Amz-SignedHeaders=host&x-id=GetObject)

