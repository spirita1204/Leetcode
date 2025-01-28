# 49. Group Anagrams

Data structure: Hash Table
Difficulty: Medium

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

```

**Example 2:**

```
Input: strs = [""]
Output: [[""]]

```

**Example 3:**

```
Input: strs = ["a"]
Output: [["a"]]
```

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {//用map做多對一概念
        Map<String, List<String>> map = new HashMap<>();
        for(int i = 0 ; i < strs.length ; i++){//索引 -> 排序的string
            char[] ar = strs[i].toCharArray();
            Arrays.sort(ar);
            String sorted = String.valueOf(ar);
            List<String> sub = map.computeIfAbsent(sorted, k -> new ArrayList<>());//computeIfAbsent慢
            sub.add(strs[i]);
            //对 hashMap 中指定 key 的值进行重新计算，如果不存在这个 key，则添加到 hashMap 中。
        }
        return new ArrayList<List<String>>(map.values());
    }
}
```