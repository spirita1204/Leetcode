# 3170. Lexicographically Minimum String After Removing Stars  

  Data Structure: Heap,Set </br> Difficulty: Medium </br> </br>You are given a string `s`. It may contain any number of `'*'` characters. Your task is to remove all `'*'` characters.

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
			  // 如果兩個字符相等，則優先返回較大的索引（這樣較晚出現的字符會被優先處理）。
				// 如果兩個字符不同，則按照字符的字典序來排序。
        Queue<Integer> pq = new PriorityQueue<>(
                (a, b) -> s.charAt(a) == s.charAt(b) ? b - a : s.charAt(a) - s.charAt(b));
        StringBuilder sb = new StringBuilder();
        // 用來存儲需要刪除的索引。當遇到星號 (*) 時，這些索引將會被標記為 "刪除"。
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

![Image](https://prod-files-secure.s3.us-west-2.amazonaws.com/81bfe8e8-c2fe-4d29-8949-0ba3cf293f0f/257c3c94-b229-4eaa-872c-b2d6343910d8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q4K3VFZ6%2F20250607%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250607T035043Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDBXsQL0XWdG9T3CiiPfABLMmmaeHdoLAjaxZotFxz1xgIhAJE1Cd9zfqg0L7%2FykZiHDEzW4l0sq0QbmYTDOnxenmZ4Kv8DCGsQABoMNjM3NDIzMTgzODA1IgxLxSoKujB6ZjO4i%2Foq3APL9nzSnn4dmuWEBTEd%2BzpquC%2FedL4BTy67kAySg%2BWyduozxZx72eDcruXc8xsvIo0CHBONsBeDn2M%2BDXunUEMkJuzXIPwLMuD59FRXSv192d50MZyWmz6HPqUD6DFX3NaGdEPqKhv0tD6ChgiWhd4o8wCJWwNvOnxu4d5e1O8VXBNJ45lw3Fu9pHonHfk1TDR6wEMyHVe6aopCLLBRiAX8uOjN5%2FRWK%2FK24UvQmPJQ8m7vkzSHnRX8iq720uk0SOb98qw7%2BlCZItzwD%2Bv0obzBpjpKv3BXCuUk%2BHDgybFedpXW1htuk9CUE7DHJCPG%2FYwz0lHrbWJ5WSTpu2rTgl0m9KEEnZZWxF1xPizjToE6c0gVpr6fsS6%2BQemAKbXxecLUGTDW6UY7q7k6spxk8d30fka0%2FBBKQ0LOdRjmdv3b8lpC1TCn8KPL8Lsw0Q3RSh1eVDuP3dYF7B3NT%2FmEQmXeQeP0JlC1y2uYaPDBOH6As0wuIVblXgDfgak26H0Kxj3n7poskCcFEZCutle8rHS8IzQeHkMUG%2Bn0udGLoee2Nh6NgUhg2urFBZ434gP51FpzFeOWQTHQWaYfm9%2BqkqBwi7B5qUVb9m85Sp8Mic4TjaAhWVOFSLERePBr5DDFwI7CBjqkAcBdJTP35Zl0CbU6bdo5TWZSMk9Wj%2F9uQjRZ3Aq2UyMdQbGVR%2FOjLPaOLLU73iaHWw%2BdLb7Kf%2Fp6%2FdyrG%2F%2FTNQBnIZ%2FRkhsqnlh%2BCGnoFpk9D%2BZxKpqpbg8zf8ZLVSMECQsnalkqxBQCdr1LUJ2%2Bb7VuivHSl0s9FGCJitz3QedH7M42o2K3vFINEOziTE3syUI5rjKxcbTd1zmtfpvc5O9pTa%2Fg&X-Amz-Signature=8bc878b4c289b28441622d4bb879c11e60a6988873d5fda8e7acbfe8511754b6&X-Amz-SignedHeaders=host&x-id=GetObject)

