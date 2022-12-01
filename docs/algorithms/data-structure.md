---
title: Data Structures
has_children: true
nav_order: 2
resource: true
desc: " Data Structures interview questions and answers."
categories: [Data Structures]
---

# Data Structures
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## LRU Cache

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:

*`LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.

*`int get(int key)` Return the value of the `key` if the `key` exists, otherwise return `-1`.

*`void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

```log
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

**Constraints:**

* 1 <= capacity <= 3000

* 0 <= key <= 104

* 0 <= value <= 105

* At most `2 * 105` calls will be made to `get` and `put`.
 
### Solution 1 : Ordered dictionary

**Intuition**

We're asked to implement `the structure` which provides the following operations in O(1) time :

* Get the key / Check if the key exists

* Put the key

* Delete the first added key

The first two operations in O(1) time are provided by the standard hashmap, and the last one - by linked list.

    There is a structure called ordered dictionary, it combines behind both hashmap and linked list.
 
#### Implementation
```java
class LRUCache extends LinkedHashMap<Integer, Integer>{
    private int capacity;
    
    public LRUCache(int capacity) {
        super(capacity, 0.75F, true);
        this.capacity = capacity;
    }

    public int get(int key) {
        return super.getOrDefault(key, -1);
    }

    public void put(int key, int value) {
        super.put(key, value);
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity; 
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

#### Complexity Analysis

**Time complexity :** O(1) both for `put` and `get` since all operations with ordered dictionary : `get/in/set/move_to_end/popitem` `(get/containsKey/put/remove)` are done in a constant time.

**Space complexity :** O(capacity) since the space is used only for an ordered dictionary with at most `capacity + 1` elements.


### Solution 2 : Hashmap + DoubleLinkedList

#### Implementation
```java
public class LRUCache {

  class DLinkedNode {
    int key;
    int value;
    DLinkedNode prev;
    DLinkedNode next;
  }

  private void addNode(DLinkedNode node) {
    /**
     * Always add the new node right after head.
     */
    node.prev = head;
    node.next = head.next;

    head.next.prev = node;
    head.next = node;
  }

  private void removeNode(DLinkedNode node){
    /**
     * Remove an existing node from the linked list.
     */
    DLinkedNode prev = node.prev;
    DLinkedNode next = node.next;

    prev.next = next;
    next.prev = prev;
  }

  private void moveToHead(DLinkedNode node){
    /**
     * Move certain node in between to the head.
     */
    removeNode(node);
    addNode(node);
  }

  private DLinkedNode popTail() {
    /**
     * Pop the current tail.
     */
    DLinkedNode res = tail.prev;
    removeNode(res);
    return res;
  }

  private Map<Integer, DLinkedNode> cache = new HashMap<>();
  private int size;
  private int capacity;
  private DLinkedNode head, tail;

  public LRUCache(int capacity) {
    this.size = 0;
    this.capacity = capacity;

    head = new DLinkedNode();
    // head.prev = null;

    tail = new DLinkedNode();
    // tail.next = null;

    head.next = tail;
    tail.prev = head;
  }

  public int get(int key) {
    DLinkedNode node = cache.get(key);
    if (node == null) return -1;

    // move the accessed node to the head;
    moveToHead(node);

    return node.value;
  }

  public void put(int key, int value) {
    DLinkedNode node = cache.get(key);

    if(node == null) {
      DLinkedNode newNode = new DLinkedNode();
      newNode.key = key;
      newNode.value = value;

      cache.put(key, newNode);
      addNode(newNode);

      ++size;

      if(size > capacity) {
        // pop the tail
        DLinkedNode tail = popTail();
        cache.remove(tail.key);
        --size;
      }
    } else {
      // update the value.
      node.value = value;
      moveToHead(node);
    }
  }
}
```

#### Complexity Analysis

**Time complexity :** O(1) both for `put` and `get`.

**Space complexity :** O(capacity) since the space is used only for a hashmap and double linked list with at most `capacity + 1` elements.

### Solution 3 : double linked list

#### Implementation
```java
class Node{
    int key;
    int value;
    Node prev;
    Node next;
 
    public Node(int key, int value){
        this.key=key;
        this.value=value;
    }
}
```
By analyzing the get and put, we can summarize there are 2 basic operations: `1) removeNode(Node t)`, `2) offerNode(Node t)`.

```java
class LRUCache {
Node head;
Node tail;
HashMap<Integer, Node> map = null;
 int cap = 0;
public LRUCache(int capacity) {
this.cap = capacity;
this.map = new HashMap<>();
}
public int get(int key) {
if(map.get(key)==null){
return -1;
}
//move to tail
Node t = map.get(key);
removeNode(t);
offerNode(t);
return t.value;
}
public void put(int key, int value) {
if(map.containsKey(key)){
Node t = map.get(key);
t.value = value;
//move to tail
removeNode(t);
offerNode(t);
}else{
if(map.size()>=cap){
//delete head
map.remove(head.key);
removeNode(head);
}
//add to tail
Node node = new Node(key, value);
offerNode(node);
map.put(key, node);
}
}
private void removeNode(Node n){
if(n.prev!=null){
n.prev.next = n.next;
}else{
head = n.next;
}
if(n.next!=null){
n.next.prev = n.prev;
}else{
tail = n.prev;
}
}
private void offerNode(Node n){
if(tail!=null){
tail.next = n;
}
n.prev = tail;
n.next = null;
tail = n;
if(head == null){
head = tail;
}
}
}
```

--- 

## Design Hit Counter

Design a hit counter which counts the number of hits received in the past `5` minutes (i.e., the past `300` seconds).

Your system should accept a `timestamp` parameter (**in seconds** granularity), and you may assume that calls are being made to the system in chronological order (i.e., `timestamp` is monotonically increasing). Several hits may arrive roughly at the same time.

Implement the HitCounter class:

*`HitCounter()` Initializes the object of the hit counter system.

*`void hit(int timestamp)` Records a hit that happened at `timestamp` (**in seconds**). Several hits may happen at the same `timestamp`.

*`int getHits(int timestamp)` Returns the number of hits in the past `5` minutes from `timestamp` (i.e., the past `300` seconds).


**Example 1:**

```log
Input
["HitCounter", "hit", "hit", "hit", "getHits", "hit", "getHits", "getHits"]
[[], [1], [2], [3], [4], [300], [300], [301]]
Output
[null, null, null, null, 3, null, 4, 3]

Explanation
HitCounter hitCounter = new HitCounter();
hitCounter.hit(1);       // hit at timestamp 1.
hitCounter.hit(2);       // hit at timestamp 2.
hitCounter.hit(3);       // hit at timestamp 3.
hitCounter.getHits(4);   // get hits at timestamp 4, return 3.
hitCounter.hit(300);     // hit at timestamp 300.
hitCounter.getHits(300); // get hits at timestamp 300, return 4.
hitCounter.getHits(301); // get hits at timestamp 301, return 3.
```


**Constraints:**

* `1 <= timestamp <= 2 * 109`

* All the calls are being made to the system in chronological order (i.e., `timestamp` is monotonically increasing).

* At most `300` calls will be made to `hit` and `getHits`.

### Solution 1 : Using Queue

**Intuition**

A key observation here is that all the timestamps that we will encounter are going to be in increasing order. Also as the timestamps' value increases we have to ignore the timestamps that occurred previously (having a difference of 300 or more with the latest timestamp). This is the case of considering the elements in the FIFO manner (First in first out) which is best solved by using the "queue" data structure.

**Algorithm**

We will add each timestamp to the queue in the hit method and will remove all the timestamps with difference greater than or equal to 300 from the queue inside getHits. The answer returned from the getHits method is then simply the size of the queue.

#### Implementation

```java
class HitCounter {
    private Queue<Integer> hits; 

    /** Initialize your data structure here. */
    public HitCounter() {
        this.hits = new LinkedList<Integer>();
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    public void hit(int timestamp) {
        this.hits.add(timestamp);
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    public int getHits(int timestamp) {
        while (!this.hits.isEmpty()) {
            int diff = timestamp - this.hits.peek();
            if (diff >= 300) this.hits.remove();
            else break;
        }
        return this.hits.size();
    }
}
```

#### Complexity Analysis

**Time Complexity**

* `hit` - Since inserting a value in the queue takes place in O(1) time, hence hit method works in O(1).

* `getHits` - Assuming a total of nn values present in the queue at a time and the total number of timestamps encountered throughout is N. In the worst case scenario, we might end up removing all the entries from the queue in getHits method if the difference in timestamp is greater than or equal to 300. Hence in the worst case, a "single" call to the `getHits` method can take O(n) time. However, we must notice that each `timestamp` is processed only twice (first while adding the timestamp in the queue in hit method and second while removing the `timestamp` from the queue in the `getHits` method). Hence if the total number of timestamps encountered throughout is N, the overall time taken by getHits method is O(N). This results in an amortized time complexity of O(1) for a single call to `getHits` method.

**Space Complexity:** Considering the total timestamps encountered throughout to be N, the queue can have upto N elements, hence overall space complexity of this approach is O(N).

### Solution 2 : Using Deque with Pairs

Consider the follow up, where we have multiple hits arriving at the "same" `timestamps`. We can optimize Approach 1 even further. In this approach, we'll not only keep the timestamps but will also keep the count of the timestamps as well. For example, if we call `hit` method `5` times for `timestamp = 1`, the queue in case of Approach 1 will look like `[1, 1, 1, 1, 1]`. This will lead to 5 removals in the `getHits` method when we remove the value `1` from the `queue`. To avoid this repetitive removals of the same value, in Approach 2, we'll store the value as `(1, 5)` where the first value `1` is the `timestamp` and the second value `5` is the count. For this, we'll use the "deque" data structure which allows us to `insert` and `delete` values from both the ends of the `queue`.

**Algorithm**

The updated algorithm in Approach 2 is as follows.

* If we encounter the `hit` for the same `timestamp`, instead of appending a new entry in the deque, we simply increment the count of the latest `timestamp`.

* In order to keep the track of total number of elements (for the last `300` seconds), we also use a variable total which we initialize to 0 and keep updating as we add or remove the elements from the queue. We increment the value of total by 1 when hit method is called and we decrement by the value of total by the count of the timestamp that we remove from the `queue`.

#### Implementation 

```java
class HitCounter {

    private int total;
    private Deque<Pair<Integer, Integer>> hits; 

    /** Initialize your data structure here. */
    public HitCounter() {
        // Initialize total to 0
        this.total = 0;
        this.hits = new LinkedList<Pair<Integer, Integer>>();
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    public void hit(int timestamp) {
        if (this.hits.isEmpty() || this.hits.getLast().getKey() != timestamp) {
            // Insert the new timestamp with count = 1
            this.hits.add(new Pair<Integer, Integer>(timestamp, 1));
        } else {
            // Update the count of latest timestamp by incrementing the count by 1

            // Obtain the current count of the latest timestamp 
            int prevCount = this.hits.getLast().getValue();
            // Remove the last pair of (timestamp, count) from the deque
            this.hits.removeLast();
            // Insert a new pair of (timestamp, updated count) in the deque
            this.hits.add(new Pair<Integer, Integer>(timestamp, prevCount + 1));
        }
        // Increment total
        this.total++;
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    public int getHits(int timestamp) {
        while (!this.hits.isEmpty()) {
            int diff = timestamp - this.hits.getFirst().getKey();
            if (diff >= 300) {
                // Decrement total by the count of the oldest timestamp
                this.total -= this.hits.getFirst().getValue();
                this.hits.removeFirst();
            }
            else break;
        }
        return this.total;
    }
}
```

#### Complexity Analysis

In the worst case, when there are not many repetitions, the time complexity and space complexity of Approach 2 is the same as Approach 1. However in case we have repetitions (say `k` repetitions of a particular `ith` timestamp), the time complexity and space complexities are as follows.

**Time Complexity:**

* `hit` - O(1).

* `getHits` - If there are a total of `n` pairs present in the deque, worst case time complexity can be O(n). However, by clubbing all the timestamps with same value together, for the `ith` timestamp with `k` repetitions, the time complexity is O(1) as here, instead of removing all those `k` repetitions, we only remove a single entry from the `deque`.

**Space complexity:** If there are a total of `N` elements that we encountered throughout, the space complexity is O(N) (similar to Approach 1). However, in the case of repetitions, the space required for storing those k values O(1).

---

## Tweet Counts Per Frequency

A social media company is trying to monitor activity on their site by analyzing the number of tweets that occur in select periods of time. These periods can be partitioned into smaller **time chunks** based on a certain frequency (every **minute**, **hour**, or **day**).

For example, the period `[10, 10000]` (in **seconds**) would be partitioned into the following time chunks with these frequencies:

* Every **minute** (60-second chunks): `[10,69]`, `[70,129]`, `[130,189]`, `...`, `[9970,10000]`

* Every **hour** (3600-second chunks): `[10,3609]`, `[3610,7209]`, `[7210,10000]`

* Every **day** (86400-second chunks): `[10,10000]`

Notice that the last chunk may be shorter than the specified frequency's chunk size and will always end with the end time of the period (`10000` in the above example).

Design and implement an API to help the company with their analysis.

Implement the `TweetCounts` class:

* `TweetCounts()` Initializes the `TweetCounts` object.

* `void recordTweet(String tweetName, int time)` Stores the `tweetName` at the recorded time (in **seconds**).

* `List<Integer> getTweetCountsPerFrequency(String freq, String tweetName, int startTime, int endTime)` Returns a list of integers representing the number of tweets with `tweetName` in each time chunk for the given period of time `[startTime, endTime]` (in **seconds**) and frequency `freq`.

   * `freq` is one of `minute`, `hour`, or `day` representing a frequency of every **minute, hour, or day** respectively.

**Example:**

```log
Input
["TweetCounts","recordTweet","recordTweet","recordTweet","getTweetCountsPerFrequency","getTweetCountsPerFrequency","recordTweet","getTweetCountsPerFrequency"]
[[],["tweet3",0],["tweet3",60],["tweet3",10],["minute","tweet3",0,59],["minute","tweet3",0,60],["tweet3",120],["hour","tweet3",0,210]]

Output
[null,null,null,null,[2],[2,1],null,[4]]

Explanation
TweetCounts tweetCounts = new TweetCounts();
tweetCounts.recordTweet("tweet3", 0);                              // New tweet "tweet3" at time 0
tweetCounts.recordTweet("tweet3", 60);                             // New tweet "tweet3" at time 60
tweetCounts.recordTweet("tweet3", 10);                             // New tweet "tweet3" at time 10
tweetCounts.getTweetCountsPerFrequency("minute", "tweet3", 0, 59); // return [2]; chunk [0,59] had 2 tweets
tweetCounts.getTweetCountsPerFrequency("minute", "tweet3", 0, 60); // return [2,1]; chunk [0,59] had 2 tweets, chunk [60,60] had 1 tweet
tweetCounts.recordTweet("tweet3", 120);                            // New tweet "tweet3" at time 120
tweetCounts.getTweetCountsPerFrequency("hour", "tweet3", 0, 210);  // return [4]; chunk [0,210] had 4 tweets
```

**Constraints:**

* `0 <= time, startTime, endTime <= 109`

* `0 <= endTime - startTime <= 104`

* There will be at most `104` calls **in total** to `recordTweet` and `getTweetCountsPerFrequency`.

### Solution 

#### Implementation

```java
class TweetCounts {
    
    private class TreeNode {
        
        private int val;
        private TreeNode left;
        private TreeNode right;
        
        private TreeNode(int data) {
            val = data;
            left = null;
            right = null;
        }
        
    }
    
    private Map<String, TreeNode> map;

    public TweetCounts() {
        map = new HashMap<>();
    }
    
    private TreeNode insert(TreeNode root, int val) {
        if (root == null) {
            root = new TreeNode(val);
        }
        else if (root.val <= val) {
            root.right = insert(root.right, val);
        }
        else {
            root.left = insert(root.left, val);
        }
        return root;
    }
    
    public void recordTweet(String name, int time) {
        TreeNode root = map.get(name);
        root = insert(root, time);
        map.put(name, root);
    }
    
    private int treverse(TreeNode root, int l, int r) {
        if (root == null || l >= r) {
            return 0;
        }
        if (root.val <= l) {
            int add = root.val == l ? 1 : 0;
            return add + treverse(root.right, l, r);
        }
        if (root.val >= r) {
            return treverse(root.left, l, r);
        }
        return 1 + treverse(root.left, l, r) + treverse(root.right, l, r);
    }
    
    public List<Integer> getTweetCountsPerFrequency(String freq, String name, int start, int end) {
        int d = 0;
        TreeNode root = map.get(name);
        List<Integer> res = new ArrayList<>();
        if (freq.equals("minute")) {
            d = 60;
        }
        else if (freq.equals("hour")) {
            d = 3600;
        }
        else {
            d = 86400;
        }
        while (start + d <= end) {
            int count = treverse(root, start, start + d);
            start = start + d;
            res.add(count);
        }
        if (start <= end) {
            int count = treverse(root, start, end + 1);
            res.add(count);
            start = end + 1;
        }
        return res;
    }
    
}
```

---

## Design Parking System

Design a parking system for a parking lot. The parking lot has three kinds of parking spaces: big, medium, and small, with a fixed number of slots for each size.

Implement the `ParkingSystem` class:

* `ParkingSystem(int big, int medium, int small)` Initializes object of the `ParkingSystem` class. The number of slots for each parking space are given as part of the constructor.

* `bool addCar(int carType)` Checks whether there is a parking space of `carType` for the car that wants to get into the parking lot. `carType` can be of three kinds: big, medium, or small, which are represented by `1`, `2`, and `3` respectively. **A car can only park in a parking space of its** `carType`. If there is no space available, return `false`, else park the car in that size space and return `true`.

**Example 1:**
```log
Input
["ParkingSystem", "addCar", "addCar", "addCar", "addCar"]
[[1, 1, 0], [1], [2], [3], [1]]
Output
[null, true, true, false, false]

Explanation
ParkingSystem parkingSystem = new ParkingSystem(1, 1, 0);
parkingSystem.addCar(1); // return true because there is 1 available slot for a big car
parkingSystem.addCar(2); // return true because there is 1 available slot for a medium car
parkingSystem.addCar(3); // return false because there is no available slot for a small car
parkingSystem.addCar(1); // return false because there is no available slot for a big car. It is already occupied.
```

**Constraints:**

* `0 <= big, medium, small <= 1000`

* `carType` is `1`, `2`, or `3`

* At most `1000` calls will be made to `addCar`

### Solution 

**Algorithm**

1. we can take 3 variables to hold count of big,med,small counts. here i have taken array of size 3 instead.

2. now just use carType-1 as index of the array and check if value present at that index > 0. if yes return true else false.

3. apart from that keep on decrementing value present on carType-1 index. since not more than 1000 calls cannot be made value decremented cannot go out of range.

#### Implementation
```java
class ParkingSystem {
    private int[] size;
    public ParkingSystem(int big, int medium, int small) {
        this.size = new int[]{big, medium, small};
    }
    
    public boolean addCar(int carType) {
        return size[carType-1]-->0;
    }
}
```

## Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of `1`s (land) and `0`s (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```log
Input: grid = [
["1","1","1","1","0"],
["1","1","0","1","0"],
["1","1","0","0","0"],
["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**

```log
Input: grid = [
["1","1","0","0","0"],
["1","1","0","0","0"],
["0","0","1","0","0"],
["0","0","0","1","1"]
]
Output: 3
```

**Constraints:**

* `m == grid.length`

* `n == grid[i].length`

* `1 <= m, n <= 300`

* `grid[i][j] is '0' or '1'`.

### Solution 1 : DFS [Accepted]

**Intuition**

Treat the 2d grid map as an undirected graph and there is an edge between two horizontally or vertically adjacent nodes of value '`1`'.

**Algorithm**

Linear scan the 2d grid map, if a node contains a '`1`', then it is a root node that triggers a Depth First Search. During DFS, every visited node should be set as '0' to mark as visited node. Count the number of root nodes that trigger DFS, this number would be the number of islands since each DFS starting at some root identifies an island.

#### Implementation

```java
class Solution {
  void dfs(char[][] grid, int r, int c) {
    int nr = grid.length;
    int nc = grid[0].length;

    if (r < 0 || c < 0 || r >= nr || c >= nc || grid[r][c] == '0') {
      return;
    }

    grid[r][c] = '0';
    dfs(grid, r - 1, c);
    dfs(grid, r + 1, c);
    dfs(grid, r, c - 1);
    dfs(grid, r, c + 1);
  }

  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    int nr = grid.length;
    int nc = grid[0].length;
    int num_islands = 0;
    for (int r = 0; r < nr; ++r) {
      for (int c = 0; c < nc; ++c) {
        if (grid[r][c] == '1') {
          ++num_islands;
          dfs(grid, r, c);
        }
      }
    }

    return num_islands;
  }
}
```

#### Complexity Analysis

**Time complexity :** O(M×N) where M is the number of rows and N is the number of columns.

**Space complexity :** worst case O(M×N) in case that the grid map is filled with lands where DFS goes by M×N deep.

### Solution 2 : BFS [Accepted]

**Algorithm**

Linear scan the 2d grid map, if a node contains a '`1`', then it is a root node that triggers a Breadth First Search. Put it into a queue and set its value as '`0`' to mark as visited node. Iteratively search the neighbors of enqueued nodes until the queue becomes empty.

#### Implementation
```java
class Solution {
  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    int nr = grid.length;
    int nc = grid[0].length;
    int num_islands = 0;

    for (int r = 0; r < nr; ++r) {
      for (int c = 0; c < nc; ++c) {
        if (grid[r][c] == '1') {
          ++num_islands;
          grid[r][c] = '0'; // mark as visited
          Queue<Integer> neighbors = new LinkedList<>();
          neighbors.add(r * nc + c);
          while (!neighbors.isEmpty()) {
            int id = neighbors.remove();
            int row = id / nc;
            int col = id % nc;
            if (row - 1 >= 0 && grid[row-1][col] == '1') {
              neighbors.add((row-1) * nc + col);
              grid[row-1][col] = '0';
            }
            if (row + 1 < nr && grid[row+1][col] == '1') {
              neighbors.add((row+1) * nc + col);
              grid[row+1][col] = '0';
            }
            if (col - 1 >= 0 && grid[row][col-1] == '1') {
              neighbors.add(row * nc + col-1);
              grid[row][col-1] = '0';
            }
            if (col + 1 < nc && grid[row][col+1] == '1') {
              neighbors.add(row * nc + col+1);
              grid[row][col+1] = '0';
            }
          }
        }
      }
    }

    return num_islands;
  }
}
```
#### Complexity Analysis

**Time complexity :** O(M×N) where M is the number of rows and N is the number of columns.

**Space complexity :** O(min(M,N)) because in worst case where the grid is filled with lands, the size of queue can grow up to min(M,N).

### Solution 3 : Union Find (aka Disjoint Set) [Accepted]

**Algorithm**

Traverse the 2d grid map and union adjacent lands horizontally or vertically, at the end, return the number of connected components maintained in the UnionFind data structure.

#### Implementation
```java
class Solution {
  class UnionFind {
    int count; // # of connected components
    int[] parent;
    int[] rank;

    public UnionFind(char[][] grid) { // for problem 200
      count = 0;
      int m = grid.length;
      int n = grid[0].length;
      parent = new int[m * n];
      rank = new int[m * n];
      for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
          if (grid[i][j] == '1') {
            parent[i * n + j] = i * n + j;
            ++count;
          }
          rank[i * n + j] = 0;
        }
      }
    }

    public int find(int i) { // path compression
      if (parent[i] != i) parent[i] = find(parent[i]);
      return parent[i];
    }

    public void union(int x, int y) { // union with rank
      int rootx = find(x);
      int rooty = find(y);
      if (rootx != rooty) {
        if (rank[rootx] > rank[rooty]) {
          parent[rooty] = rootx;
        } else if (rank[rootx] < rank[rooty]) {
          parent[rootx] = rooty;
        } else {
          parent[rooty] = rootx; rank[rootx] += 1;
        }
        --count;
      }
    }

    public int getCount() {
      return count;
    }
  }

  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    int nr = grid.length;
    int nc = grid[0].length;
    int num_islands = 0;
    UnionFind uf = new UnionFind(grid);
    for (int r = 0; r < nr; ++r) {
      for (int c = 0; c < nc; ++c) {
        if (grid[r][c] == '1') {
          grid[r][c] = '0';
          if (r - 1 >= 0 && grid[r-1][c] == '1') {
            uf.union(r * nc + c, (r-1) * nc + c);
          }
          if (r + 1 < nr && grid[r+1][c] == '1') {
            uf.union(r * nc + c, (r+1) * nc + c);
          }
          if (c - 1 >= 0 && grid[r][c-1] == '1') {
            uf.union(r * nc + c, r * nc + c - 1);
          }
          if (c + 1 < nc && grid[r][c+1] == '1') {
            uf.union(r * nc + c, r * nc + c + 1);
          }
        }
      }
    }

    return uf.getCount();
  }
}
```
#### Complexity Analysis

**Time complexity :** O(M×N) where M is the number of rows and N is the number of columns. Note that Union operation takes essentially constant time[1] when UnionFind is implemented with both path compression and union by rank.

**Space complexity :** O(M×N) as required by UnionFind data structure.

### Solution 4 : Very concise Java AC solution

#### Implementation
```java
public class Solution {

  private int n;
  private int m;

  public int numIslands(char[][] grid) {
    int count = 0;
    n = grid.length;
    if (n == 0) return 0;
    m = grid[0].length;
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++)
        if (grid[i][j] == '1') {
          DFSMarking(grid, i, j);
          ++count;
        }
    }
    return count;
  }

  private void DFSMarking(char[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] != '1') return;
    grid[i][j] = '0';
    DFSMarking(grid, i + 1, j);
    DFSMarking(grid, i - 1, j);
    DFSMarking(grid, i, j + 1);
    DFSMarking(grid, i, j - 1);
  }
}
```

### Solution 5 : Java DFS and BFS solution

**DFS:**
```java
public class solution{
    public int numIslands(char[][] grid) {
    int count=0;
    for(int i=0;i<grid.length;i++)
        for(int j=0;j<grid[0].length;j++){
            if(grid[i][j]=='1'){
                dfsFill(grid,i,j);
                count++;
            }
        }
    return count;
}
private void dfsFill(char[][] grid,int i, int j){
    if(i>=0 && j>=0 && i<grid.length && j<grid[0].length&&grid[i][j]=='1'){
        grid[i][j]='0';
        dfsFill(grid, i + 1, j);
        dfsFill(grid, i - 1, j);
        dfsFill(grid, i, j + 1);
        dfsFill(grid, i, j - 1);
    }
}
        }
```

**BFS:**

```java
public class solution {
  public int numIslands(char[][] grid) {
    int count = 0;
    for (int i = 0; i < grid.length; i++)
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == '1') {
          bfsFill(grid, i, j);
          count++;
        }
      }
    return count;
  }

  private void bfsFill(char[][] grid, int x, int y) {
    grid[x][y] = '0';
    int n = grid.length;
    int m = grid[0].length;
    LinkedList<Integer> queue = new LinkedList<Integer>();
    int code = x * m + y;
    queue.offer(code);
    while (!queue.isEmpty()) {
      code = queue.poll();
      int i = code / m;
      int j = code % m;
      if (i > 0 && grid[i - 1][j] == '1')    //search upward and mark adjacent '1's as '0'.
      {
        queue.offer((i - 1) * m + j);
        grid[i - 1][j] = '0';
      }
      if (i < n - 1 && grid[i + 1][j] == '1')  //down
      {
        queue.offer((i + 1) * m + j);
        grid[i + 1][j] = '0';
      }
      if (j > 0 && grid[i][j - 1] == '1')  //left
      {
        queue.offer(i * m + j - 1);
        grid[i][j - 1] = '0';
      }
      if (j < m - 1 && grid[i][j + 1] == '1')  //right
      {
        queue.offer(i * m + j + 1);
        grid[i][j + 1] = '0';
      }
    }
  }
}
```
---

## Design Search Autocomplete System

Design a search autocomplete system for a search engine. Users may input a sentence (at least one word and end with a special character `#`).

You are given a string array `sentences` and an integer array `times` both of length `n` where `sentences[i]` is a previously typed sentence and `times[i]` is the corresponding number of times the sentence was typed. For each input character except `#`, return the top `3` historical hot sentences that have the same prefix as the part of the sentence already typed.

Here are the specific rules:

* The hot degree for a sentence is defined as the number of times a user typed the exactly same sentence before.

* The returned top `3` hot sentences should be sorted by hot degree (The first is the hottest one). If several sentences have the same hot degree, use ASCII-code order (smaller one appears first).

* If less than `3` hot sentences exist, return as many as you can.

* When the input is a special character, it means the sentence ends, and in this case, you need to return an empty list.

Implement the `AutocompleteSystem` class:

* `AutocompleteSystem(String[] sentences, int[] times)` Initializes the object with the `sentences` and times `arrays`.

* `List<String> input(char c)` This indicates that the user typed the character `c`.

* Returns an empty array `[]` if `c == '#'` and stores the inputted sentence in the system.

* Returns the top `3` historical hot sentences that have the same prefix as the part of the sentence already typed. If there are fewer than 3 matches, return them all.


**Example 1:**

```log
Input
["AutocompleteSystem", "input", "input", "input", "input"]
[[["i love you", "island", "iroman", "i love leetcode"], [5, 3, 2, 2]], ["i"], [" "], ["a"], ["#"]]
Output
[null, ["i love you", "island", "i love leetcode"], ["i love you", "i love leetcode"], [], []]

Explanation
AutocompleteSystem obj = new AutocompleteSystem(["i love you", "island", "iroman", "i love leetcode"], [5, 3, 2, 2]);
obj.input("i"); // return ["i love you", "island", "i love leetcode"]. There are four sentences that have prefix "i". Among them, "ironman" and "i love leetcode" have same hot degree. Since ' ' has ASCII code 32 and 'r' has ASCII code 114, "i love leetcode" should be in front of "ironman". Also we only need to output top 3 hot sentences, so "ironman" will be ignored.
obj.input(" "); // return ["i love you", "i love leetcode"]. There are only two sentences that have prefix "i ".
obj.input("a"); // return []. There are no sentences that have prefix "i a".
obj.input("#"); // return []. The user finished the input, the sentence "i a" should be saved as a historical sentence in system. And the following input will be counted as a new search.

```

**Constraints:**

* `n == sentences.length`

* `n == times.length`

* `1 <= n <= 100`

* `1 <= sentences[i].length <= 100`

* `1 <= times[i] <= 50`

* `c` is a lowercase English letter, a hash `#`, or space '`  `'.

* Each tested sentence will be a sequence of characters `c` that end with the character `#`.

* Each tested sentence will have a length in the range `[1, 200]`.

* The words in each input sentence are separated by single spaces.

* At most `5000` calls will be made to `input`.

### Solution 

Only thing more than a normal `Trie` is added a map of `sentence` to `count` in each of the `Trie` node to facilitate process of getting top 3 results.


#### Implementation
```java
public class AutocompleteSystem {
    class TrieNode {
        Map<Character, TrieNode> children;
        Map<String, Integer> counts;
        boolean isWord;
        public TrieNode() {
            children = new HashMap<Character, TrieNode>();
            counts = new HashMap<String, Integer>();
            isWord = false;
        }
    }
    
    class Pair {
        String s;
        int c;
        public Pair(String s, int c) {
            this.s = s; this.c = c;
        }
    }
    
    TrieNode root;
    String prefix;
    
    
    public AutocompleteSystem(String[] sentences, int[] times) {
        root = new TrieNode();
        prefix = "";
        
        for (int i = 0; i < sentences.length; i++) {
            add(sentences[i], times[i]);
        }
    }
    
    private void add(String s, int count) {
        TrieNode curr = root;
        for (char c : s.toCharArray()) {
            TrieNode next = curr.children.get(c);
            if (next == null) {
                next = new TrieNode();
                curr.children.put(c, next);
            }
            curr = next;
            curr.counts.put(s, curr.counts.getOrDefault(s, 0) + count);
        }
        curr.isWord = true;
    }
    
    public List<String> input(char c) {
        if (c == '#') {
            add(prefix, 1);
            prefix = "";
            return new ArrayList<String>();
        }
        
        prefix = prefix + c;
        TrieNode curr = root;
        for (char cc : prefix.toCharArray()) {
            TrieNode next = curr.children.get(cc);
            if (next == null) {
                return new ArrayList<String>();
            }
            curr = next;
        }
        
        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> (a.c == b.c ? a.s.compareTo(b.s) : b.c - a.c));
        for (String s : curr.counts.keySet()) {
            pq.add(new Pair(s, curr.counts.get(s)));
        }

        List<String> res = new ArrayList<String>();
        for (int i = 0; i < 3 && !pq.isEmpty(); i++) {
            res.add(pq.poll().s);
        }
        return res;
    }
}
```
---

## Frog Jump

A frog is crossing a river. The river is divided into some number of units, and at each unit, there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of `stones`' positions (in units) in sorted **ascending order**, determine if the frog can cross the river by landing on the last stone. Initially, the frog is on the first stone and assumes the first jump must be `1` unit.

If the frog's last jump was `k` units, its next jump must be either `k - 1`, `k`, or `k + 1` units. The frog can only jump in the forward direction.

**Example 1:**
```log
Input: stones = [0,1,3,5,6,8,12,17]
Output: true
Explanation: The frog can jump to the last stone by jumping 1 unit to the 2nd stone, then 2 units to the 3rd stone, then 2 units to the 4th stone, then 3 units to the 6th stone, 4 units to the 7th stone, and 5 units to the 8th stone.
```
**Example 2:**
```log
Input: stones = [0,1,2,3,4,8,9,11]
Output: false
Explanation: There is no way to jump to the last stone as the gap between the 5th and 6th stone is too large.
```
 
**Constraints:**

* `2 <= stones.length <= 2000`

* `0 <= stones[i] <= 231 - 1`

* `stones[0] == 0`

* `stones` is sorted in a strictly increasing order.

### Solution 1 : Brute Force [Time Limit Exceeded]

In the brute force approach, we make use of a recursive function `canCross` which takes the given stone array, the current position and the current `jumpsize` as input arguments. We start with `currentPosition=0` and `jumpsize=0`. Then for every function call, we start from the `currentPosition` and check if there lies a stone at` (currentPostion + newjumpsize)`, where, the `newjumpsize` could be `jumpsize`, `jumpsize+1` or `jumpsize-1`. In order to check whether a stone exists at the specified positions, we check the elements of the array in a linear manner. If a stone exists at any of these positions, we call the recursive function again with the same stone array, the `currentPosition` and the `newjumpsize` as the parameters. If we are able to reach the end of the stone array through any of these calls, we return `true` to indicate the possibility of reaching the end.

#### Implementation

```java
public class Solution {
    public boolean canCross(int[] stones) {
        return can_Cross(stones, 0, 0);
    }
    public boolean can_Cross(int[] stones, int ind, int jumpsize) {
        for (int i = ind + 1; i < stones.length; i++) {
            int gap = stones[i] - stones[ind];
            if (gap >= jumpsize - 1 && gap <= jumpsize + 1) {
                if (can_Cross(stones, i, gap)) {
                    return true;
                }
            }
        }
        return ind == stones.length - 1;
    }
}public class Solution {
    public boolean canCross(int[] stones) {
        return can_Cross(stones, 0, 0);
    }
    public boolean can_Cross(int[] stones, int ind, int jumpsize) {
        for (int i = ind + 1; i < stones.length; i++) {
            int gap = stones[i] - stones[ind];
            if (gap >= jumpsize - 1 && gap <= jumpsize + 1) {
                if (can_Cross(stones, i, gap)) {
                    return true;
                }
            }
        }
        return ind == stones.length - 1;
    }
}
```

#### Complexity Analysis

**Time complexity :** O(3^n). Recursion tree can grow upto 3^n.

**Space complexity :** O(n). Recursion of depth n is used.

### Solution 2 : Better Brute Force[Time Limit Exceeded]

**Algorithm**

In the previous brute force approach, we need to find if a stone exists at (currentPosition + new jumpsize), where newjumpsize could be either of jumpsize-1, jumpsize or jumpsize+1. But in order to check if a stone exists at the specified location, we searched the given array in linearly. To optimize this, we can use binary search to look for the element in the given array since it is sorted. Rest of the method remains the same.

#### Implementation 

```java

public class Solution {
    public boolean canCross(int[] stones) {
        return can_Cross(stones, 0, 0);
    }
    public boolean can_Cross(int[] stones, int ind, int jumpsize) {
        if (ind == stones.length - 1) {
            return true;
        }
        int ind1 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize);
        if (ind1 >= 0 && can_Cross(stones, ind1, jumpsize)) {
            return true;
        }
        int ind2 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize - 1);
        if (ind2 >= 0 && can_Cross(stones, ind2, jumpsize - 1)) {
            return true;
        }
        int ind3 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize + 1);
        if (ind3 >= 0 && can_Cross(stones, ind3, jumpsize + 1)) {
            return true;
        }
        return false;
    }
}
```

#### Complexity Analysis

**Time complexity :** O(3^n) . Recursion tree can grow upto 3^n.

**Space complexity :** O(n). Recursion of depth n is used.

### Solution 3 :  Using Memoization [Accepted]

**Algorithm**

Another problem with above approaches is that we can make the same function calls coming through different paths e.g. For a given `currentIndex`, we can call the recursive function `canCross` with the `jumpsize`, say n. This nn could be resulting from previous `jumpsize` being `n-1`,`n` or `n+1`. Thus, many redundant function calls could be made prolonging the running time. This redundancy can be removed by making use of memoization. We make use of a `2-d` `memo` array, initialized by `−1s`, to store the result returned from a function call for a particular `currentIndex` and `jumpsize`. If the same `currentIndex` and `jumpsize` happens is encountered again, we can return the result directly using the `memo` array. This helps to prune the search tree to a great extent.

#### Implementation

```java
public class Solution {
    public boolean canCross(int[] stones) {
        int[][] memo = new int[stones.length][stones.length];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return can_Cross(stones, 0, 0, memo) == 1;
    }
    public int can_Cross(int[] stones, int ind, int jumpsize, int[][] memo) {
        if (memo[ind][jumpsize] >= 0) {
            return memo[ind][jumpsize];
        }
        for (int i = ind + 1; i < stones.length; i++) {
            int gap = stones[i] - stones[ind];
            if (gap >= jumpsize - 1 && gap <= jumpsize + 1) {
                if (can_Cross(stones, i, gap, memo) == 1) {
                    memo[ind][gap] = 1;
                    return 1;
                }
            }
        }
        memo[ind][jumpsize] = (ind == stones.length - 1) ? 1 : 0;
        return memo[ind][jumpsize];
    }
}
```

#### Complexity Analysis

**Time complexity :** O(n^3). Memoization will reduce time complexity to O(n^3).

**Space complexity :** O(n^2). `memo` matrix of size n^2 is used.

### Solution 4 : Using Memoization with Binary Search [Accepted]

**Algorithm**

We can optimize the above memoization approach, if we make use of Binary Search to find if a stone exists at currentPostion + newjumpsize instead of searching linearly.

#### Implementation

```java
public class Solution {
    public boolean canCross(int[] stones) {
        int[][] memo = new int[stones.length][stones.length];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return can_Cross(stones, 0, 0, memo) == 1;
    }
    public int can_Cross(int[] stones, int ind, int jumpsize, int[][] memo) {
        if (memo[ind][jumpsize] >= 0) {
            return memo[ind][jumpsize];
        }
        int ind1 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize);
        if (ind1 >= 0 && can_Cross(stones, ind1, jumpsize, memo) == 1) {
            memo[ind][jumpsize] = 1;
            return 1;
        }
        int ind2 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize - 1);
        if (ind2 >= 0 && can_Cross(stones, ind2, jumpsize - 1, memo) == 1) {
            memo[ind][jumpsize - 1] = 1;
            return 1;
        }
        int ind3 = Arrays.binarySearch(stones, ind + 1, stones.length, stones[ind] + jumpsize + 1);
        if (ind3 >= 0 && can_Cross(stones, ind3, jumpsize + 1, memo) == 1) {
            memo[ind][jumpsize + 1] = 1;
            return 1;
        }
        memo[ind][jumpsize] = ((ind == stones.length - 1) ? 1 : 0);
        return memo[ind][jumpsize];
    }
}
```
#### Complexity Analysis

**Time complexity :** O(n^2 log(n)). We traverse the complete dp matrix once (O(n^2)). For every entry we take atmost n numbers as pivot.

**Space complexity :** O(n^2). dp matrix of size n^2 is used.

### Solution 5 : Using Dynamic Programming[Accepted]

**Algorithm**

In the DP Approach, we make use of a hashmap `map` which contains `key:value` pairs such that key refers to the position at which a stone is present and value is a set containing the `jumpsize` which can lead to the current stone position. We start by making a hashmap whose `keys` are all the positions at which a stone is present and the `values` are all empty except position 0 whose value contains 0. Then, we start traversing the elements(positions) of the given stone array in sequential order. For the `currentPosition`, for every possible `jumpsize` in the `value` set, we check if `currentPosition + newjumpsize` exists in the `map`, where `newjumpsize` can be either `jumpsize-1`, `jumpsize`, `jumpsize+1`. If so, we append the corresponding `value` set with `newjumpsize`. We continue in the same manner. If at the end, the `value` set corresponding to the last position is non-empty, we conclude that reaching the end is possible, otherwise, it isn't.

#### Implementation

```java
public class Solution {
    public boolean canCross(int[] stones) {
        HashMap<Integer, Set<Integer>> map = new HashMap<>();
        for (int i = 0; i < stones.length; i++) {
            map.put(stones[i], new HashSet<Integer>());
        }
        map.get(0).add(0);
        for (int i = 0; i < stones.length; i++) {
            for (int k : map.get(stones[i])) {
                for (int step = k - 1; step <= k + 1; step++) {
                    if (step > 0 && map.containsKey(stones[i] + step)) {
                        map.get(stones[i] + step).add(step);
                    }
                }
            }
        }
        return map.get(stones[stones.length - 1]).size() > 0;
    }
}
```

#### Complexity Analysis

**Time complexity :** O(n^2). Two nested loops are there.

**Space complexity :** O(n^2). `hashmap` size can grow upto n^2.

### Solution 6 : short DP solution

#### Implementation

```java
class Solution {
    public boolean canCross(int[] stones) {
        Map<Integer, Set<Integer>> dp = new HashMap();
        
        for(int val: stones) dp.put(val, new HashSet());
        dp.get(stones[0]).add(1);
        
        for(int val: stones){
            for(int jump: dp.get(val)){
                if(jump!= 0 && dp.containsKey(val+jump)){
                    dp.get(val+jump).add(jump-1);
                    dp.get(val+jump).add(jump);
                    dp.get(val+jump).add(jump+1);
                }
            }
        }
        
        return !dp.get(stones[stones.length-1]).isEmpty();
    }
}
```

---

## Subdomain Visit Count






















