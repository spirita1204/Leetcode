# 1948. Delete Duplicate Folders in System  

  Methods: DFS </br> Difficulty: Hard </br> </br>Due to a bug, there are many duplicate folders in a file system. You are given a 2D array `paths`, where `paths[i]` is an array representing an absolute path to the `ith` folder in the file system.

- For example, `["one", "two", "three"]` represents the path `"/one/two/three"`.
Two folders (not necessarily on the same level) are **identical** if they contain the **same non-empty** set of identical subfolders and underlying subfolder structure. The folders **do not** need to be at the root level to be identical. If two or more folders are **identical**, then **mark** the folders as well as all their subfolders.

- For example, folders `"/a"` and `"/b"` in the file structure below are identical. They (as well as their subfolders) should **all** be marked:
- However, if the file structure also included the path `"/b/w"`, then the folders `"/a"` and `"/b"` would not be identical. Note that `"/a/x"` and `"/b/x"` would still be considered identical even with the added folder.
Once all the identical folders and their subfolders have been marked, the file system will **delete** all of them. The file system only runs the deletion once, so any folders that become identical after the initial deletion are not deleted.

Return *the 2D array *`ans` *containing the paths of the ****remaining**** folders after deleting all the marked folders. The paths may be returned in ****any**** order*.

**Example 1:   **

![Image](https://assets.leetcode.com/uploads/2021/07/19/lc-dupfolder1.jpg)

```plain text
Input: paths = [["a"],["c"],["d"],["a","b"],["c","b"],["d","a"]]
Output: [["d"],["d","a"]]
Explanation: The file structure is as shown.
Folders "/a" and "/c" (and their subfolders) are marked for deletion because they both contain an empty
folder named "b".
```

**Example 2:**

![Image](https://assets.leetcode.com/uploads/2021/07/19/lc-dupfolder2.jpg)

```plain text
Input: paths = [["a"],["c"],["a","b"],["c","b"],["a","b","x"],["a","b","x","y"],["w"],["w","y"]]
Output: [["c"],["c","b"],["a"],["a","b"]]
Explanation:The file structure is as shown.
Folders "/a/b/x" and "/w" (and their subfolders) are marked for deletion because they both contain an empty folder named "y".
Note that folders "/a" and "/c" are identical after the deletion, but they are not deleted because they were not marked beforehand.
```

**Example 3:**

![Image](https://assets.leetcode.com/uploads/2021/07/19/lc-dupfolder3.jpg)

```plain text
Input: paths = [["a","b"],["c","d"],["c"],["a"]]
Output: [["c"],["c","d"],["a"],["a","b"]]
Explanation: All folders are unique in the file system.
Note that the returned array can be in a different order as the order does not matter.
```

**Constraints:**

- `1 <= paths.length <= 2 * 104`
- `1 <= paths[i].length <= 500`
- `1 <= paths[i][j].length <= 10`
- `1 <= sum(paths[i][j].length) <= 2 * 105`
- `path[i][j]` consists of lowercase English letters.
- No two paths lead to the same folder.
- For any folder not at the root level, its parent folder will also be in the input.
```java
class Solution {
    static class Node {
        String name;
        TreeMap<String, Node> children;
        String signature;

        public Node(String name) {
            this.name = name;
            this.children = new TreeMap<>();
        }
    }

    public List<List<String>> deleteDuplicateFolder(List<List<String>> paths) {
        // 組 node
        Node root = new Node("");
        for (List<String> path : paths) {
            Node curr = root;
            for (String folder : path) {
                curr.children.putIfAbsent(folder, new Node(folder));
                curr = curr.children.get(folder);
            }
        }

        Map<String, Integer> countMap = new HashMap<>();
        dfs(root, countMap);

        List<List<String>> result = new ArrayList<>();
        List<String> currentPath = new ArrayList<>();
        // countMap = {b()=2, a()=1, a(b())c(b())d(a())=1}
        for (Node child : root.children.values()) {
            dfs2(child, currentPath, result, countMap);
        }
        return result;
    }

    private void dfs(Node node, Map<String, Integer> countMap) {
        if (node.children.isEmpty()) {
            node.signature = "";
            return;
        }
        StringBuilder sb = new StringBuilder();
        for (Node child : node.children.values()) {
            dfs(child, countMap);
            sb.append(child.name).append('(').append(child.signature).append(')');
        }
        node.signature = sb.toString();
        countMap.put(node.signature, countMap.getOrDefault(node.signature, 0) + 1);
    }
    
    // 跳過重複子樹
    private void dfs2(Node node, List<String> currentPath, List<List<String>> result, Map<String, Integer> countMap) {
        // 空資料夾就算 signature 一樣，也不能刪, 只有「有子資料夾」的節點才會被刪
        if (!node.children.isEmpty() && countMap.getOrDefault(node.signature, 0) >= 2) {
            return;
        }
        currentPath.add(node.name);
        result.add(new ArrayList<>(currentPath));
        for (Node child : node.children.values()) {
            dfs2(child, currentPath, result, countMap);
        }
        currentPath.remove(currentPath.size() - 1);
    }
}
```

