# 731. My Calendar II  

  Data Structure: Set </br> Difficulty: Medium </br> </br>You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a **triple booking**.

A **triple booking** happens when three events have some non-empty intersection (i.e., some moment is common to all the three events.).

The event can be represented as a pair of integers `start` and `end` that represents a booking on the half-open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

Implement the `MyCalendarTwo` class:

- `MyCalendarTwo()` Initializes the calendar object.
- `boolean book(int start, int end)` Returns `true` if the event can be added to the calendar successfully without causing a **triple booking**. Otherwise, return `false` and do not add the event to the calendar.
**Example 1:**

```plain text
Input
["MyCalendarTwo", "book", "book", "book", "book", "book", "book"]
[[], [10, 20], [50, 60], [10, 40], [5, 15], [5, 10], [25, 55]]
Output
[null, true, true, true, false, true, true]

Explanation
MyCalendarTwo myCalendarTwo = new MyCalendarTwo();
myCalendarTwo.book(10, 20); // return True, The event can be booked.
myCalendarTwo.book(50, 60); // return True, The event can be booked.
myCalendarTwo.book(10, 40); // return True, The event can be double booked.
myCalendarTwo.book(5, 15);  // return False, The event cannot be booked, because it would result in a triple booking.
myCalendarTwo.book(5, 10); // return True, The event can be booked, as it does not use time 10 which is already double booked.
myCalendarTwo.book(25, 55); // return True, The event can be booked, as the time in [25, 40) will be double booked with the third event, the time [40, 50) will be single booked, and the time [50, 55) will be double booked with the second event.

```

**Constraints:**

- `0 <= start < end <= 109`
- At most `1000` calls will be made to `book`.
```java
class MyCalendarTwo {
    Set<Pair> calendar1;// 存所有區間
    Set<Pair> calendar2;// 存有交集區間

    public MyCalendarTwo() {
        calendar1 = new HashSet<>();
        calendar2 = new HashSet<>();
    }

    public boolean book(int start, int end) {
        // 遍歷 以有交集過兩次區間 如果有何其重疊 代表第三次 return false
        for (Pair p: calendar2) {
            if (start >= p.right || end <= p.left) // 沒有交集
                continue;
            return false;
        }
        // 遍歷 所有區間 有交集地方存到calendar2
        for (Pair p: calendar1) {
            if (start >= p.right || end <= p.left) // 沒有交集
                continue;
            // 有交集(放入有交集區段) (start, key)最大 (end, value)最小
            calendar2.add(new Pair(Math.max(start, p.left), Math.min(end, p.right)));
        }
        calendar1.add(new Pair(start, end));
        
        return true;
    }
}

class Pair {
    int left;
    int right;

    public Pair(int left, int right) {
        this.left = left;
        this.right = right;
    }
}
/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo obj = new MyCalendarTwo();
 * boolean param_1 = obj.book(start,end);
 */
```

