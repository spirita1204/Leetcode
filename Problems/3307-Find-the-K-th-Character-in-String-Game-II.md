# 3307. Find the K-th Character in String Game II  

  Methods: Math </br> Data Structure: Queue </br> Difficulty: Hard </br> </br>Alice and Bob are playing a game. Initially, Alice has a string `word = "a"`.

You are given a **positive** integer `k`. You are also given an integer array `operations`, where `operations[i]` represents the **type** of the `ith` operation.

Now Bob will ask Alice to perform **all** operations in sequence:

- If `operations[i] == 0`, **append** a copy of `word` to itself.
- If `operations[i] == 1`, generate a new string by **changing** each character in `word` to its **next** character in the English alphabet, and **append** it to the *original* `word`. For example, performing the operation on `"c"` generates `"cd"` and performing the operation on `"zb"` generates `"zbac"`.
Return the value of the `kth` character in `word` after performing all the operations.

**Note** that the character `'z'` can be changed to `'a'` in the second type of operation.

**Example 1:**

**Input:** k = 5, operations = [0,0,0]

**Output:** "a"

**Explanation:**

Initially, `word == "a"`. Alice performs the three operations as follows:

- Appends `"a"` to `"a"`, `word` becomes `"aa"`.
- Appends `"aa"` to `"aa"`, `word` becomes `"aaaa"`.
- Appends `"aaaa"` to `"aaaa"`, `word` becomes `"aaaaaaaa"`.
**Example 2:**

**Input:** k = 10, operations = [0,1,0,1]

**Output:** "b"

**Explanation:**

Initially, `word == "a"`. Alice performs the four operations as follows:

- Appends `"a"` to `"a"`, `word` becomes `"aa"`.
- Appends `"bb"` to `"aa"`, `word` becomes `"aabb"`.
- Appends `"aabb"` to `"aabb"`, `word` becomes `"aabbaabb"`.
- Appends `"bbccbbcc"` to `"aabbaabb"`, `word` becomes `"aabbaabbbbccbbcc"`.
**Constraints:**

- `1 <= k <= 1014`
- `1 <= operations.length <= 100`
- `operations[i]` is either 0 or 1.
- The input is generated such that `word` has **at least** `k` characters after all operations.
```java
class Solution {
    public char kthCharacter(long k, int[] operations) {
        int shift = 0; 
        List<Long> lengths = new ArrayList<>();
        long len = 1;

        for (int op : operations) {
            len *= 2;
            lengths.add(len);
            if (len >= k) break;
        }

        for (int i = lengths.size() - 1; i >= 0; i--) {
            long half = lengths.get(i) / 2;// ˇ
            int op = operations[i];

            if (k > half) {
                k -= half; // 如果 k 在字串的後半部分，那麼更新 k 的位置
                if (op == 1) shift++; // 如果操作是 1，字母進行了偏移，增加偏移量
            }
            // else: k remains the same
        }

        // Apply total shift from 'a'
        return (char) ((shift % 26) + 'a');
    }
}
```

