# 729. My Calendar I

Data structure: Hash Table
Difficulty: Medium

Medium

Topics

Companies

Hint

You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a **double booking**.

A **double booking** happens when two events have some non-empty intersection (i.e., some moment is common to both events.).

The event can be represented as a pair of integers `start` and `end` that represents a booking on the half-open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

Implement the `MyCalendar` class:

- `MyCalendar()` Initializes the calendar object.
- `boolean book(int start, int end)` Returns `true` if the event can be added to the calendar successfully without causing a **double booking**. Otherwise, return `false` and do not add the event to the calendar.

**Example 1:**

```
Input
["MyCalendar", "book", "book", "book"]
[[], [10, 20], [15, 25], [20, 30]]
Output
[null, true, false, true]

Explanation
MyCalendar myCalendar = new MyCalendar();
myCalendar.book(10, 20); // return True
myCalendar.book(15, 25); // return False, It can not be booked because time 15 is already booked by another event.
myCalendar.book(20, 30); // return True, The event can be booked, as the first event takes every time less than 20, but not including 20.
```

**Constraints:**

- `0 <= start < end <= 109`
- At most `1000` calls will be made to `book`.

我解法 : 

Runtime **56**ms **Beats32.36%of users with Java**

Memory **44.64**MB **Beats30.68%of users with Java**

```java
class MyCalendar {
    List<Pair> lists;

    public MyCalendar() {
        lists = new ArrayList<Pair>();
    }
    
    public boolean book(int start, int end) {
        for(Pair p: lists) {
            boolean res = isOverLap(start, end, p.getLeft(), p.getRight());
            if(res) return false;
        }
        lists.add(new Pair(start, end));

        return true;
    }

    /** 根據傳入兩時間軸 判斷是否有交集 */
    private boolean isOverLap(int s1, int e1, int s2, int e2) {
        return Math.max(s1, s2) < Math.min(e1, e2);
    }
}

class Pair {
    int left;
    int right;

    public Pair(int left, int right) {
        this.left = left;
        this.right = right;
    }
    public int getLeft() { return left; }
    public int getRight() { return right; }
}

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar obj = new MyCalendar();
 * boolean param_1 = obj.book(start,end);
 */
```

優化 :

Runtime  **20**ms         Beats**73.22%**of users with Java

Memory  **44.69**MB   Beats**30.68%**of users with Java

```java
class MyCalendar {
    TreeMap<Integer, Integer> calendar;// 有序的map 會依key做排序;相對set list 快

    public MyCalendar() {
        calendar = new TreeMap<>();
    }

    public boolean book(int start, int end) {
        Integer floorKey = calendar.floorKey(start);// 返回的最大鍵小於等於key，或者null
        if (floorKey != null && calendar.get(floorKey) > start) return false;// 有交集
        Integer ceilingKey = calendar.ceilingKey(start);// 返回最小鍵大於或等於返回到給定的鍵，或nul
        if (ceilingKey != null && ceilingKey < end) return false;// 有交集

        calendar.put(start, end);
        return true;
    }
}
```