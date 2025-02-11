# 2424. Longest Uploaded Prefix

Data structure: Union Find
Difficulty: Medium

Medium

Topics

Companies

Hint

You are given a stream of `n` videos, each represented by a **distinct** number from `1` to `n` that you need to "upload" to a server. You need to implement a data structure that calculates the length of the **longest uploaded prefix** at various points in the upload process.

We consider `i` to be an uploaded prefix if all videos in the range `1` to `i` (**inclusive**) have been uploaded to the server. The longest uploaded prefix is the **maximum** value of `i` that satisfies this definition.

Implement the `LUPrefix` class:

- `LUPrefix(int n)` Initializes the object for a stream of `n` videos.
- `void upload(int video)` Uploads `video` to the server.
- `int longest()` Returns the length of the **longest uploaded prefix** defined above.

**Example 1:**

```
Input
["LUPrefix", "upload", "longest", "upload", "longest", "upload", "longest"]
[[4], [3], [], [1], [], [2], []]
Output
[null, null, 0, null, 1, null, 3]

Explanation
LUPrefix server = new LUPrefix(4);   // Initialize a stream of 4 videos.
server.upload(3);                    // Upload video 3.
server.longest();                    // Since video 1 has not been uploaded yet, there is no prefix.
                                     // So, we return 0.
server.upload(1);                    // Upload video 1.
server.longest();                    // The prefix [1] is the longest uploaded prefix, so we return 1.
server.upload(2);                    // Upload video 2.
server.longest();                    // The prefix [1,2,3] is the longest uploaded prefix, so we return 3.

```

**Constraints:**

- `1 <= n <= 105`
- `1 <= video <= n`
- All values of `video` are **distinct**.
- At most `2 * 105` calls **in total** will be made to `upload` and `longest`.
- At least one call will be made to `longest`.

```java
class LUPrefix {
    UnionFind unionFind;
    Set<Integer> seen;

    public LUPrefix(int n) {
        seen = new HashSet<>();
        seen.add(0);
        unionFind = new UnionFind(n);
    }

    public void upload(int video) {
        seen.add(video);
        if (seen.contains(video - 1))// 有前一位 則Union
            unionFind.unite(video - 1, video);
        if (seen.contains(video + 1))
            unionFind.unite(video, video + 1);
    }

    public int longest() {
        return unionFind.findComponent(0);
    }
}

class UnionFind {
    int[] component;
    int distinctComponents;

    public UnionFind(int n) {
        component = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            component[i] = i;
        } // {0,1,2,3,4}
        distinctComponents = n;// 4
    }

    // unite. For example, if previously we have component {0, 4, 4, 4, 4, 6, 7, 7},
    // then invoke this method with a=1, b=5, then after invoke, {0, 4, 4, 4, 5, 7,
    // 7, 7}
    public boolean unite(int a, int b) {
        if (findComponent(a) != findComponent(b)) {
            component[findComponent(a)] = b;
            distinctComponents--;
            return true;
        }
        return false;// 已經相連
    }

    // find and change component
    // for example, if previously we have component: {0, 2, 3, 4, 4, 6, 7, 7}, then
    // after invoke this method with a=1, the component become {0, 4, 4, 4, 4, 6, 7,
    // 7}
    // 找到 input 節點的 root ，可以藉此確定 input 節點屬於哪一個子集
    public int findComponent(int a) {
        if (component[a] != a) {
            component[a] = findComponent(component[a]);
        }
        return component[a];
    }
}
/**
 * Your LUPrefix object will be instantiated and called as such:
 * LUPrefix obj = new LUPrefix(n);
 * obj.upload(video);
 * int param_2 = obj.longest();
 */
```