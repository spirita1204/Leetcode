# 1207. Unique Number of Occurrences

Data structure: Hash Table, Set
Difficulty: Easy

Given an array of integers `arr`, return `true` *if the number of occurrences of each value in the array is **unique** or* `false` *otherwise*.

**Example 1:**

```
Input: arr = [1,2,2,1,1,3]
Output: true
Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.
```

**Example 2:**

```
Input: arr = [1,2]
Output: false

```

**Example 3:**

```
Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]
Output: true

```

**Constraints:**

- `1 <= arr.length <= 1000`
- `1000 <= arr[i] <= 1000`

```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i <arr.length; i++) {
            int num = arr[i];
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        return hasDuplicateValues(map);
    }

    private boolean hasDuplicateValues(Map<Integer, Integer> map) {
        // 使用HashSet存储值，如果出现重复值会自动去重
        HashSet<Object> set = new HashSet<>(map.values());
        return set.size() == map.values().size();
    }
}
```