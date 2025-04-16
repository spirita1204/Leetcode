# 1442. Count Triplets That Can Form Two Arrays of Equal XOR  

  Methods: Bitwise,Prefix Sum </br> Difficulty: Medium </br> </br>prefix xor

Given an array of integers `arr`.

We want to select three indices `i`, `j` and `k` where `(0 <= i < j <= k < arr.length)`.

Let's define `a` and `b` as follows:

- `a = arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1]`
- `b = arr[j] ^ arr[j + 1] ^ ... ^ arr[k]`
Note that **^** denotes the **bitwise-xor** operation.

Return *the number of triplets* (`i`, `j` and `k`) Where `a == b`.

**Example 1:**

```plain text
Input: arr = [2,3,1,6,7]
Output: 4
Explanation: The triplets are (0,1,2), (0,2,2), (2,3,4) and (2,4,4)

```

**Example 2:**

```plain text
Input: arr = [1,1,1,1,1]
Output: 10

```

**Constraints:**

- `1 <= arr.length <= 300`
- `1 <= arr[i] <= 108`
```java
class Solution {
    public int countTriplets(int[] arr) {
        // 自己xor自己 = 0
        // We only need to find out how many pair (i, k) of prefix value are equal.
        // Because we once we determine the pair (i,k),
        // j can be any number that i < j <= k,
        // so we need to plus k - i - 1 to the result res.
        // arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1] ^ arr[j] ^ arr[j + 1] ^ ... ^ arr[k] = 0
        // prefix[k+1] = prefix[i] 結論
        int n = arr.length + 1, res = 0;
        int[] prefix = new int[n];

        for (int i = 1; i < n; i++)// prefix xor
            prefix[i] = arr[i - 1] ^ prefix[i - 1];
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (prefix[i] == prefix[j])
                    res += j - i - 1;

        return res;
    }
}
```

