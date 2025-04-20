# 781. Rabbits in Forest  

  Methods: Math,Greedy </br> Data Structure: Hash Table </br> Difficulty: Medium </br> </br>There is a forest with an unknown number of rabbits. We asked n rabbits **"How many rabbits have the same color as you?"** and collected the answers in an integer array `answers` where `answers[i]` is the answer of the `ith` rabbit.

Given the array `answers`, return *the minimum number of rabbits that could be in the forest*.

**Example 1:**

```plain text
Input: answers = [1,1,2]
Output: 5
Explanation:
The two rabbits that answered "1" could both be the same color, say red.
The rabbit that answered "2" can't be red or the answers would be inconsistent.
Say the rabbit that answered "2" was blue.
Then there should be 2 other blue rabbits in the forest that didn't answer into the array.
The smallest possible number of rabbits in the forest is therefore 5: 3 that answered plus 2 that didn't.
```

**Example 2:**

```plain text
Input: answers = [10,10,10]
Output: 11
```

**Constraints:**

- `1 <= answers.length <= 1000`
- `0 <= answers[i] < 1000`
```java
class Solution {
    public int numRabbits(int[] answers) {
        Map<Integer, Integer> hm = new HashMap<>();
        int len = answers.length;

        for(int i = 0; i < len; i++) // (answers[0], cnt)
            hm.put(answers[i], hm.getOrDefault(answers[i], 0) + 1); 
        
        int res = 0;

        for(int key: hm.keySet()) {
            int val = hm.get(key);
            int groupMax = key + 1;

            if(val <= groupMax) // 同一群組
                res += (key + 1);
            else {
                int nGroup = val / groupMax;
                int r = val % groupMax;
                res += (groupMax * nGroup + ((r != 0) ? groupMax : 0));
            }
        }
        return res;
    }
}
```

