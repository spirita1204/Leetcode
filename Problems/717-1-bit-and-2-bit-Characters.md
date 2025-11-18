# 717. 1-bit and 2-bit Characters  

  Methods: Basic logic </br> Difficulty: Easy </br> </br>We have two special characters:

- The first character can be represented by one bit `0`.
- The second character can be represented by two bits (`10` or `11`).
Given a binary array `bits` that ends with `0`, return `true` if the last character must be a one-bit character. 

**Example 1:**

```plain text
Input: bits = [1,0,0]
Output: true
Explanation: The only way to decode it is two-bit character and one-bit character.
So the last character is one-bit character.
```

**Example 2:**

```plain text
Input: bits = [1,1,1,0]
Output: false
Explanation: The only way to decode it is two-bit character and two-bit character.
So the last character is not one-bit character.
```

**Constraints:**

- `1 <= bits.length <= 1000`
- `bits[i]` is either `0` or `1`.
```java
class Solution {
    public boolean isOneBitCharacter(int[] bits) {
        int ones = 0;
        //Starting from one but last, as last one is always 0.
        for (int i = bits.length - 2; i >= 0 && bits[i] != 0 ; i--) { 
            ones++;
        }
        if (ones % 2 > 0) return false; 
        return true;
    }
}
```

