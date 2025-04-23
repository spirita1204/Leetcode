# 1399. Count Largest Group  

  Data Structure: Hash Table </br> Difficulty: Easy </br> </br>You are given an integer `n`.

Each number from `1` to `n` is grouped according to the sum of its digits.

Return *the number of groups that have the largest size*.

**Example 1:**

```plain text
Input: n = 13
Output: 4
Explanation: There are 9 groups in total, they are grouped according sum of its digits of numbers from 1 to 13:
[1,10], [2,11], [3,12], [4,13], [5], [6], [7], [8], [9].
There are 4 groups with largest size.
```

**Example 2:**

```plain text
Input: n = 2
Output: 2
Explanation: There are 2 groups [1], [2] of size 1.
```

**Constraints:**

- `1 <= n <= 104`
```sql
class Solution {
    public int countLargestGroup(int n) {
        List<List<Integer>> list = new ArrayList<>();
        for (int i = 0; i <= 36; i++) { // sum of digits can go up to 36
            list.add(new ArrayList<>());
        }

        int max = 0;
        for (int i = 1; i <= n; i++) {
            int sum = sumofdigit(i);
            list.get(sum).add(i);
            max = Math.max(max, list.get(sum).size());
        }
        int count = 0;
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).size() == max) {
                count++;
            }
        }

        return count;
    }

    public int sumofdigit(int n) {
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n = n / 10;
        }
        return sum;
    }
}
```

