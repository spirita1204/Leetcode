# 451. Sort Characters By Frequency

Methods: Sort
Data structure: Heap
Difficulty: Medium

Medium

Topics

Companies

Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return *the sorted string*. If there are multiple answers, return *any of them*.

**Example 1:**

```
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.

```

**Example 2:**

```
Input: s = "cccaaa"
Output: "aaaccc"
Explanation: Both 'c' and 'a' appear three times, so both "cccaaa" and "aaaccc" are valid answers.
Note that "cacaca" is incorrect, as the same characters must be together.

```

**Example 3:**

```
Input: s = "Aabb"
Output: "bbAa"
Explanation: "bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.

```

**Constraints:**

- `1 <= s.length <= 5 * 105`
- `s` consists of uppercase and lowercase English letters and digits.

```java
class Solution {
    public String frequencySort(String s) {
        int[] letters = new int[127];// 表示A~Z, a~z 0~9
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> letters[b] - letters[a]);
        StringBuilder sb = new StringBuilder();

        for(char c : s.toCharArray()) {
            letters[c - '0']++;
        }
        for(int i = 0; i < letters.length; i++) {
            if(letters[i] != 0) 
                pq.offer(i);
        }
        while(!pq.isEmpty()) {
            int letter = pq.poll();
            for(int i = 0; i < letters[letter]; i++) 
                sb.append((char)(letter + 48));// Ascii: 0 : 48 
        }
        return sb.toString();
    }
}
```

bucket sort 

```java
class Solution {
    public String frequencySort(String s) {

        // max priority queue O(nlogn) ,frequency map O(n)
        // TC O(nlogn)

        // TC O(N) with array withut sorting

        Map<Character, Integer> mp = new HashMap<>();
        for (char c : s.toCharArray())
            mp.put(c, mp.getOrDefault(c, 0) + 1); // freq map done for each characters of string

        List<Character> bucket[] = new List[s.length() + 1]; // bucket array of type list of characters (Array of lists)

        for (Character key : mp.keySet()) {
            int freq = mp.get(key);
            if (bucket[freq] == null) {
                bucket[freq] = new ArrayList<>();
            }
            bucket[freq].add(key);
        }
        StringBuilder sb = new StringBuilder();

        for (int i = bucket.length - 1; i >= 0; i--) {
            if (bucket[i] != null) {
                for (char c : bucket[i]) {
                    for (int j = 0; j < i; j++) { // i or mp.get(c) is same which is frequency of that character in that
                                                  // index of array present has occurred that no.. of times
                        sb.append(c);
                    }
                }
            }
        }
        return sb.toString();
    }
}
```