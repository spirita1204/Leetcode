# 846. Hand of Straights  

  Data Structure: Hash Table </br> Difficulty: Medium </br> Similar: 1296 </br> </br># Medium

Topics

Companies

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `ith` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

**Example 1:**

```plain text
Input: hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
Output: true
Explanation: Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]

```

**Example 2:**

```plain text
Input: hand = [1,2,3,4,5], groupSize = 4
Output: false
Explanation: Alice's hand can not be rearranged into groups of 4.


```

**Constraints:**

- `1 <= hand.length <= 104`
- `0 <= hand[i] <= 109`
- `1 <= groupSize <= hand.length`
**Note:** This question is the same as 1296: [https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/](https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/)

```java
class Solution {
    public boolean isNStraightHand(int[] hand, int groupSize) {
        if(hand.length % groupSize != 0) return false;
        Arrays.sort(hand);
        //[1,2,2,3,3,4,6,7,8]
        Map<Integer, Integer> hm = new HashMap<>();
        for(int i = 0; i < hand.length; i++) {
            hm.put(hand[i], hm.getOrDefault(hand[i], 0) + 1);
        }
        for(int i = 0; i < hand.length; i++) {
            if(hm.get(hand[i]) > 0) {
                for(int j = 0; j < groupSize; j++) {
                    if(hm.get(hand[i] + j) == null || hm.get(hand[i] + j) == 0) return false;
                    else hm.put(hand[i] + j, hm.get(hand[i] + j)- 1);
                }
            }
        }
        return true;
    }
}
```

