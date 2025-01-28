# 2564. Substring XOR Queries

Data structure: Hash Table
Difficulty: Medium

You are given a **binary string** `s`, and a **2D** integer array `queries` where `queries[i] = [firsti, secondi]`.

For the `ith` query, find the **shortest substring** of `s` whose **decimal value**, `val`, yields `secondi` when **bitwise XORed** with `firsti`. In other words, `val ^ firsti == secondi`.

The answer to the `ith` query is the endpoints (**0-indexed**) of the substring `[lefti, righti]` or `[-1, -1]` if no such substring exists. If there are multiple answers, choose the one with the **minimum** `lefti`.

*Return an array* `ans` *where* `ans[i] = [lefti, righti]` *is the answer to the* `ith` *query.*

A **substring** is a contiguous non-empty sequence of characters within a string.

**Example 1:**

```
Input: s = "101101", queries = [[0,5],[1,2]]
Output: [[0,2],[2,3]]
Explanation: For the first query the substring in range[0,2] is"101" which has a decimal value of5, and5 ^ 0 = 5, hence the answer to the first query is[0,2]. In the second query, the substring in range[2,3] is"11", and has a decimal value of3, and3 ^ 1 = 2. So,[2,3] is returned for the second query.

```

**Example 2:**

```
Input: s = "0101", queries = [[12,8]]
Output: [[-1,-1]]
Explanation: In this example there is no substring that answers the query, hence[-1,-1] is returned.

```

**Example 3:**

```
Input: s = "1", queries = [[4,5]]
Output: [[0,0]]
Explanation: For this example, the substring in range[0,0] has a decimal value of1, and1 ^ 4 = 5. So, the answer is[0,0].

```

**Constraints:**

- `1 <= s.length <= 104`
- `s[i]` is either `'0'` or `'1'`.
- `1 <= queries.length <= 105`
- `0 <= firsti, secondi <= 109`

```java
class Solution {
    public int[][] substringXorQueries(String s, int[][] queries) {
        Map<Integer,int[]> map = new HashMap<>(); 
        List<int[]> res = new ArrayList<>();
        int count = 0;//計算0出現第一次位置       
        // <個二進位轉D的數字,放頭 尾>
        for(int i = 0 ;i< s.length() ; i++){//遍例所有開始投
            if(s.charAt(i)  == '0'){
                if(count < 1){//當第一次出現0;
                    count++;
                    map.put(0,new int[]{i,i});//將0第一次出現位置放入
                }
                continue;
            }
            for(int length = 1; length <= 30; length++){//計算長度最長就30 因為0 <= firsti, secondi <= 10^9  對於二進胃就是30位元 技巧
                if(i + length <= s.length()){//避免超出長度
                    String number = s.substring(i,i + length);
                    System.out.println(number);
                    int b2d = Integer.valueOf(number, 2);//將找到的數字轉為10進位
                    if(!map.containsKey(b2d)){
                        map.put(b2d,new int[]{i,i + length-1});
                    }
                }
            }
        }
        for (int[] i : queries) {
            int search = i[0] ^ i[1];
            res.add((map.get(search) == null) ? new int[]{-1,-1} : map.get(search));//如果沒找到就放[-1,-1]
        }
        return res.stream().toArray(int[][]::new);
    }
}
```