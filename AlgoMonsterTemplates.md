
1. Backtracking
2. Binary Search
3. BFS on Tree
4. DFS on Tree
5. BFS on Graphs
6. DFS on Graphs
7. BFS on Matrix
8. Mono Stack
9. Topolgical Sort
10. Trie
11. Union Find
12. Merge Intervals
13. Two Pointer Template

## Templates from AlgoMonster

1. Backtracking 
```java 
private static void dfs(List<T> state, List<List<T>> res) {
    if (isSolution(state)) {
        res.add(new ArrayList<>(state)); // add a copy of the state to the result
        return;
    }
    for (T choice : choices) {
        state.add(choice);
        dfs(state, res);
        state.remove(state.size() - 1);
    }
}
```
2. Binary Search
```java 
public static int binarySearch(List<Integer> arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr.get(mid) == target) return mid;
        if (arr.get(mid) < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

```
3. BFS on Tree
```java 
public Node bfs(Node root) {
    ArrayDeque<Node> queue = new ArrayDeque<>();
    queue.add(root);
    while (queue.size() > 0) {
        Node node = queue.poll();
        for (Node child : node.children) {
            if (isGoal(child)) {
                return FOUND(child);
            }
            queue.add(child);
        }
    }
    return NOT_FOUND;
}

```
4. DFS on Tree
```java 
public static Node dfs(Node root, int target) {
    if (root == null) return null;
    if (root.val == target) {
        return root;
    }
    Node left = dfs(root.left, target);
    if (left != null) {
        return left;
    }
    return dfs(root.right, target);
}

```
5. BFS on Graphs
```java 
public void bfs(Node root) {
    ArrayDeque<Node> queue = new ArrayDeque<>();
    queue.add(root);
    Set<Node> visited = new HashSet<>();
    visited.add(root);
    while (queue.size() > 0) {
        Node node = queue.pop();
        for (Node neighbor : getNeighbors(node)) {
            if (visited.contains(neighbor)) {
                continue;
            }
            queue.add(neighbor);
            visited.add(neighbor);
        }
    }
}

```
6. DFS on Graphs
```java 
public void dfs(Node root, Set<Node> visited) {
    for (Node neighbor : node.neighbors) {
        if (visited.contains(node)) {
            continue;
        }
        visited.add(neighbor);
        dfs(neighbor, visited);
    }
}

```
7. BFS on Matrix
```java 
public int numRows = grid.length;
public int numCols = grid[0].length;

public List<Coordinate> getNeighbors(Coordinate coord) {
    int row = coord.row;
    int col = coord.col;
    int[] deltaRow = {-1, 0, 1, 0};
    int[] deltaCol = {0, 1, 0, -1};
    List<Coordinate> res = new ArrayList<>();
    for (int i = 0; i < deltaRow.length; i++) {
        int neighborRow = row + deltaRow[i];
        int neighborCol = col + deltaCol[i];
        if (0 <= neighborRow && neighborRow < numRows &&
            0 <= neighborCol && neighborCol < numCols) {
                res.add(new Coordinate(neighborRow, neighborCol));
            }
    }
    return res;
}

public void bfs(Coordinate startingNode) {
    Deque<Coordinate> queue = new ArrayDeque<>();
    queue.add(startingNode);
    Set<Coordinate> visited = new HashSet<>();
    visited.add(startingNode);

    while (queue.size() > 0) {
        Coordinate node = queue.pop();
        for (Coordinate neighbor : getNeighbors(node)) {
            if (visited.contains(neighbor)) continue;
            // Do stuff with the node if required
            // ...
            queue.add(neighbor);
            visited.add(neighbor);
        }
    }
}

```
8. Mono Stack
```java 
public static void monoStack(List<Integer> insertEntries) {
    ArrayList<Integer> stack;
    for (int entry : insertEntries) {
        while (!stack.isEmpty() && stack.get(stack.size() - 1) <= entry) {
            stack.remove(stack.size() - 1);
            // Do something with the popped item here
        }
        stack.add(entry);
    }
}

```
9. Topolgical Sort
```java 
public static <T> Map<T, Integer> countParents(Map<T, List<T>> graph) {
    Map<T, Integer> counts = new HashMap<>();
    graph.keySet().forEach(node -> {
        counts.put(node, 0);
    });
    graph.entrySet().forEach(entry -> {
        for (T node : entry.getValue()) {
            counts.put(node, counts.get(node) + 1);
        }
    });
    return counts;
}

public static <T> List<T> topoSort(Map<T, List<T>> graph) {
    List<T> res = new ArrayList<>();
    Queue<T> q = new ArrayDeque<>();
    Map<T, Integer> counts = countParents(graph);
    counts.entrySet().forEach(entry -> {
        if (entry.getValue() == 0) {
            q.add(entry.getKey());
        }
    });
    while (!q.isEmpty()) {
        T node = q.poll();
        res.add(node);
        for (T child : graph.get(node)) {
            counts.put(child, counts.get(child) - 1);
            if (counts.get(child) == 0) {
                q.add(child);
            }
        }
    }
    return res;
}

```
10. Trie
```java
public static class Node {
    char value;
    HashMap<Character, Node> children = new HashMap<>();
    public Node(char value) {
        this.value = value;
    }
    void insert(String s, int idx) {   
        if (idx == s.length()) {
            return;
        }
        if (children.containsKey(s.charAt(idx))) {
            children.get(s.charAt(idx)).insert(s, idx + 1);
        }
        else {
            children.put(s.charAt(idx), new Node(s.charAt(idx)));
            children.get(s.charAt(idx)).insert(s, idx + 1);
        }
    }
}

```
11. Union Find
```java 
public static class UnionFind<T> {
    private HashMap<T, T> id = new HashMap<>();

    public T find(T x) {
        T y = id.getOrDefault(x, x);
        if (y != x) {
            y = find(y);
            id.put(x, y);
        }
        return y;
    }

    public void union(T x, T y) {
        id.put(find(x), find(y));
    }
}

```

12. Merge Intervals

```java
public static boolean overlap(List<Integer> a, List<Integer> b) {
        return !(a.get(1) < b.get(0) || a.get(0) > b.get(1));
    }

    public static List<List<Integer>> mergeIntervals(List<List<Integer>> intervals) {
        intervals.sort((i1, i2) -> Integer.compare(i1.get(0), i2.get(0)));

        List<List<Integer>> res = new ArrayList<>();
        for (List<Integer> interval : intervals) {
            if (res.isEmpty() || !overlap(res.get(res.size() - 1), interval)) {
                res.add(interval);
            } else {
                List<Integer> lastInterval = res.get(res.size() - 1);
                lastInterval.set(1, Math.max(lastInterval.get(1), interval.get(1)));
            }
        }

        return res;
    }
```

13. Two pointer template

```java
public class Solution {
    public List<Integer> slidingWindowTemplateByHarryChaoyangHe(String s, String t) {
        //init a collection or int value to save the result according the question.
        List<Integer> result = new LinkedList<>();
        if(t.length()> s.length()) return result;
        
        //create a hashmap to save the Characters of the target substring.
        //(K, V) = (Character, Frequence of the Characters)
        Map<Character, Integer> map = new HashMap<>();
        for(char c : t.toCharArray()){
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        //maintain a counter to check whether match the target string.
        int counter = map.size();//must be the map size, NOT the string size because the char may be duplicate.
        
        //Two Pointers: begin - left pointer of the window; end - right pointer of the window
        int begin = 0, end = 0;
        
        //the length of the substring which match the target string.
        int len = Integer.MAX_VALUE; 
        
        //loop at the begining of the source string
        while(end < s.length()){
            
            char c = s.charAt(end);//get a character
            
            if( map.containsKey(c) ){
                map.put(c, map.get(c)-1);// plus or minus one
                if(map.get(c) == 0) counter--;//modify the counter according the requirement(different condition).
            }
            end++;
            
            //increase begin pointer to make it invalid/valid again
            while(counter == 0 /* counter condition. different question may have different condition */){
                
                char tempc = s.charAt(begin);//***be careful here: choose the char at begin pointer, NOT the end pointer
                if(map.containsKey(tempc)){
                    map.put(tempc, map.get(tempc) + 1);//plus or minus one
                    if(map.get(tempc) > 0) counter++;//modify the counter according the requirement(different condition).
                }
                
                /* save / update(min/max) the result if find a target*/
                // result collections or result int value
                
                begin++;
            }
        }
        return result;
    }
}
```

```java
public class TrieNode {
        public Map<Character, TrieNode> children;
        public boolean isEnd;
        
        public TrieNode() {
            this.children = new HashMap<>();
            this.isEnd = false;
        }
    }
```

```java
public class TrieNode {
        public Map<Character, TrieNode> children;
        public boolean isEnd;
        
        public TrieNode() {
            this.children = new HashMap<>();
            this.isEnd = false;
        }
    }
    
    TrieNode root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        root = new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
        TrieNode node = root;
        for (Character c: word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
                
            }
            node = node.children.get(c);
        }
        node.isEnd = true;
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        TrieNode node = root;
        return wildcardSearch(node, word, 0);
    }
    
    public boolean wildcardSearch(TrieNode node, String word, int index) {
        char[] charArray = word.toCharArray();
        for (int i = index; i<charArray.length; i++) {
            char c = charArray[i];
            if (c == '.') {
                for (Character cc: node.children.keySet()) {
                    if (wildcardSearch(node.children.get(cc), word, i+1)) {
                        return true;
                    }
                }
                return false;
            } else {
                if (node.children.containsKey(c)) {
                    node = node.children.get(c);
                } else {
                    return false;
                }
            }
        }
        return node.isEnd;
    }

```
