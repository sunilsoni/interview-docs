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













