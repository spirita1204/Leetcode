# 1792. Maximum Average Pass Ratio

Data structure: Heap
Difficulty: Medium

There is a school that has classes of students and each class will be having a final exam. You are given a 2D integer array `classes`, where `classes[i] = [passi, totali]`. You know beforehand that in the `ith` class, there are `totali` total students, but only `passi` number of students will pass the exam.

You are also given an integer `extraStudents`. There are another `extraStudents` brilliant students that are **guaranteed** to pass the exam of any class they are assigned to. You want to assign each of the `extraStudents` students to a class in a way that **maximizes** the **average** pass ratio across **all** the classes.

The **pass ratio** of a class is equal to the number of students of the class that will pass the exam divided by the total number of students of the class. The **average pass ratio** is the sum of pass ratios of all the classes divided by the number of the classes.

Return *the **maximum** possible average pass ratio after assigning the* `extraStudents` *students.* Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

```
Input: classes = [[1,2],[3,5],[2,2]],extraStudents = 2
Output: 0.78333
Explanation: You can assign the two extra students to the first class. The average pass ratio will be equal to (3/4 + 3/5 + 2/2) / 3 = 0.78333.

```

**Example 2:**

```
Input: classes = [[2,4],[3,9],[4,5],[2,10]],extraStudents = 4
Output: 0.53485
```

```java
class Solution {
    public double maxAverageRatio(int[][] classes, int extraStudents) {
        // 0.5 0.66 0.75 (0,75, 0.6 , 1)
        // 0.6 0.66      (0.66, 0.66, 1)
        // a[0] / a[1] 比較 a[0] + 1/ a[1] + 1
        Queue<int[]> pq = new PriorityQueue<>(
            (a, b) -> Double.compare(getIncrement(b), getIncrement(a))
        ); 
        for(int[] clazz: classes) {
            pq.offer(clazz);
        }
        while(extraStudents-- > 0) {
            int[] e = pq.poll();
            pq.offer(new int[] {e[0] + 1, e[1] + 1});
        }
        double res = 0;
        while(pq.size() > 0) {
            int[] e = pq.poll();
            res += (double)e[0] / e[1];
        }
        return res / classes.length;
    }
    private double getIncrement(int[] e){
        return (e[0] + 1.0) / (e[1] + 1) - (double)e[0] / e[1];
    }
}
```