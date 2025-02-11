# 56. Merge Intervals

Methods: Pointer
Difficulty: Medium

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

```

**Example 2:**

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.

```

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);//先做排序
        int pointer = 0;
        int listPointer = 0;

        for(int i = 1;i<intervals.length;i++){
            if(intervals[i][0] - intervals[i - 1][1] <= 0){//merge
                pointer = i;
                intervals[i][0] = intervals[i-1][0]; 
                intervals[i][1] = Math.max(intervals[i-1][1], intervals[i][1]);
            }else{//un interact
                list.add(new ArrayList<>());
                list.get(listPointer).add(intervals[pointer][0]);
                list.get(listPointer).add(intervals[pointer][1]);
                pointer++;
                listPointer++;
            }
        }
        list.add(new ArrayList<>());
        list.get(listPointer).add(intervals[pointer][0]);
        list.get(listPointer).add(intervals[pointer][1]);

        int[][] res = list.stream().map(  u  ->  u.stream().mapToInt(i->i).toArray()  ).toArray(int[][]::new);

        return res;
    }
}
```

2024/6/20

```java
class Solution {
	public int[][] merge(int[][] intervals) {
		// Sort by ascending starting point
		Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));

		List<int[]> result = new ArrayList<>();
		int[] newInterval = intervals[0];
		result.add(newInterval);
		for (int[] interval : intervals) {
			if (interval[0] <= newInterval[1]) // Overlapping intervals, move the end if needed
				newInterval[1] = Math.max(newInterval[1], interval[1]);
			else {                             // Disjoint intervals, add the new interval to the list
				newInterval = interval;
				result.add(newInterval);
			}
		}

		return result.toArray(new int[result.size()][]);
	}
}
```