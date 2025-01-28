# 57. Insert Interval

Methods: Pointer
Difficulty: Medium

**Medium**

8.1K

560

Companies

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` *after the insertion*.

**Example 1:**

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

```

**Example 2:**

```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

```

**Constraints:**

- `0 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 105`
- `intervals` is sorted by `starti` in **ascending** order.
- `newInterval.length == 2`
- `0 <= start <= end <= 105`

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int p1 = -1, p2 = -1;//指前面//指後面
        int x = Integer.MAX_VALUE, y = Integer.MIN_VALUE;//區間左最小//區間右最大
        List<List<Integer>> list = new ArrayList<>();

        if(intervals.length == 0) return new int[][]{newInterval};
        for(int i = 0;i< intervals.length; i++){
            if(intervals[i][0] <= newInterval[0] && intervals[i][1] >= newInterval[0]) p1 = i;
            if(intervals[i][0] <= newInterval[1] && intervals[i][1] >= newInterval[1]) p2 = i;
            if(p2 != -1 && p2<intervals.length && intervals[i][1] < newInterval[1]) p2++;
            if(p1 != -1 || p2 != -1){
                if(p1 == -1) p1 = p2;
                if(p2 == -1) p2 = p1;
                x = Math.min(intervals[p1][0], newInterval[0]); 
                y = Math.max(intervals[p2][1], newInterval[1]);
            }
        }
        System.out.print(p1+"|"+p2+"|"+x+"|"+y);
        int index = 0, listIndex = 0;
        while(index < intervals.length){//有交集情況
            if(newInterval[0]<intervals[index][0] && newInterval[1]>intervals[index][1]){//new 包含他 不做
                index++;
                continue;
            }
            list.add(new ArrayList<>());
            if(index >= p1 && index <= p2){
                list.get(listIndex).add(x);
                list.get(listIndex).add(y);
                index += (p2 - p1);//跳過不用掃
            }else{
                list.get(listIndex).add(intervals[index][0]);
                list.get(listIndex).add(intervals[index][1]);
            }
            index++;
            listIndex++;
        }
        if(p1 == -1 && p2 == -1){
            list.add(new ArrayList<>());
            list.get(listIndex).add(newInterval[0]);
            list.get(listIndex).add(newInterval[1]);
        }
        
        int[][] res = list.stream().map(  u  ->  u.stream().mapToInt(i->i).toArray()  ).toArray(int[][]::new);
        Arrays.sort(res, (a, b) -> a[0] - b[0]);//先做排序
        return res;
    }
}
```