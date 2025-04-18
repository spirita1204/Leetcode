# 38. Count and Say  

  Methods: DFS </br> Difficulty: Medium </br> </br>The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:  

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the run-length encoding of `countAndSay(n - 1)`.
[Run-length encoding](http://en.wikipedia.org/wiki/Run-length_encoding) (RLE) is a string compression method that works by replacing consecutive identical characters (repeated 2 or more times) with the concatenation of the character and the number marking the count of the characters (length of the run). For example, to compress the string `"3322251"` we replace `"33"` with `"23"`, replace `"222"` with `"32"`, replace `"5"` with `"15"` and replace `"1"` with `"11"`. Thus the compressed string becomes `"23321511"`.

Given a positive integer `n`, return *the *`nth`* element of the ****count-and-say**** sequence*.

**Example 1:**

**Input:** n = 4

**Output:** "1211"

**Explanation:**

```plain text
countAndSay(1) = "1"
countAndSay(2) = RLE of "1" = "11"
countAndSay(3) = RLE of "11" = "21"
countAndSay(4) = RLE of "21" = "1211"
```

**Example 2:**

**Input:** n = 1

**Output:** "1"

**Explanation:**

This is the base case.

**Constraints:**

- `1 <= n <= 30`
**Follow up:**

Could you solve it iteratively?

```java
class Solution {
    public String countAndSay(int n) {
        LinkedList<Integer> prevSeq = new LinkedList<Integer>();
        prevSeq.add(1);
        // Using -1 as the delimiter
        prevSeq.add(-1);

        List<Integer> finalSeq = nextSequence(n, prevSeq);
        StringBuilder seqStr = new StringBuilder();

        for (int digit : finalSeq) 
            seqStr.append(String.valueOf(digit));
        
        return seqStr.toString();
    }

    private LinkedList<Integer> nextSequence(int n, LinkedList<Integer> prevSeq) {
        if (n <= 1) {
            // remove the delimiter before return
            prevSeq.pollLast();
            return prevSeq;
        }

        LinkedList<Integer> nextSeq = new LinkedList<Integer>();
        Integer prevDigit = null;
        int digitCnt = 0;
        for (int digit : prevSeq) { //遍歷linked list同while(list.pollFirst() != null)
            if (prevDigit == null) { //數字頭 開始
                prevDigit = digit;
                digitCnt += 1; //count repetive 
            } else if (digit == prevDigit) {
                // in the middle of the sub-sequence
                digitCnt += 1;
            } else {
                // end of a sub-sequence
                nextSeq.add(digitCnt);
                nextSeq.add(prevDigit);
                // reset for the next sub-sequence
                prevDigit = digit;
                digitCnt = 1;
            }
        }

        // add the delimiter for the next recursion
        nextSeq.add(-1);

        return this.nextSequence(n - 1, nextSeq);
    }
}
```

