# 986. Interval List Intersections

Methods: Pointer
Difficulty: Medium

**Medium**

5.1K

99

Companies

You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return *the intersection of these two interval lists*.

A **closed interval** `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

**Example 1:**

![https://assets.leetcode.com/uploads/2019/01/30/interval1.png](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```
Input: firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]

```

**Example 2:**

```
Input: firstList = [[1,3],[5,9]], secondList = []
Output: []

```

**Constraints:**

- `0 <= firstList.length, secondList.length <= 1000`
- `firstList.length + secondList.length >= 1`
- `0 <= starti < endi <= 109`
- `endi < starti+1`
- `0 <= startj < endj <= 109`
- `endj < startj+1`

```jsx
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        if(firstList.length == 0 || secondList.length == 0) return new int[0][0];
        int i = 0;
        int j = 0;
        int startMax = 0, endMin = 0;
        List<int[]> res = new ArrayList<>();
        
        while(i< firstList.length && j< secondList.length){
            startMax = Math.max(firstList[i][0], secondList[j][0]);
            endMin = Math.min(firstList[i][1], secondList[j][1]);
             
			if(endMin >= startMax){//有交集 
                res.add(new int[]{startMax,endMin});
            }
			//the interval with min end has been covered completely and have no chance to intersect with any other interval so move that list's pointer
            if(endMin == firstList[i][1]) i++;       
            if(endMin == secondList[j][1]) j++;
        }
        return res.toArray(new int[res.size()][2]);
    }
}
```