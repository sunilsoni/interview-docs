---
layout: default
title: Dynamic Programming
parent: Data Structures
resource: true
desc: "Dynamic Programming interview questions and answers."
categories: [Dynamic Programming]

---

# Dynamic Programming
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

## Course Schedule II

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return *any* of them. If it is impossible to finish all courses, return *an empty array*.


**Example 1:**
```log
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```

**Example 2:**
```log
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```

**Example 3:**
```log
Input: numCourses = 1, prerequisites = []
Output: [0]
```

**Constraints:**

* `1 <= numCourses <= 2000`

* `0 <= prerequisites.length <= numCourses * (numCourses - 1)`

* `prerequisites[i].length == 2`

* `0 <= ai, bi < numCourses`

* `ai != bi`

* All the pairs `[ai, bi]` are *distinct*.

### Solution 1 : Using Depth First Search

**Intuition**

Suppose we are at a node in our graph during the depth first traversal. Let's call this node `A`.

    The way DFS would work is that we would consider all possible paths stemming from A before finishing up the recursion for A and moving onto other nodes. All the nodes in the paths stemming from the node A would have A as an ancestor. The way this fits in our problem is, all the courses in the paths stemming from the course `A` would have A as a prerequisite.

Now we know how to get all the courses that have a particular course as a prerequisite. If a valid ordering of courses is possible, the course A would come before all the other set of courses that have it as a prerequisite. This idea for solving the problem can be explored using depth first search. Let's look at the pseudo-code before looking at the formal algorithm.
```log
➔ let S be a stack of courses
➔ function dfs(node)
➔     for each neighbor in adjacency list of node
➔          dfs(neighbor)
➔     add node to S
```
Let's now look at the formal algorithm based on this idea.


**Algorithm**

1. Initialize a stack `S` that will contain the topologically sorted order of the courses in our graph.

2. Construct the adjacency list using the edge pairs given in the input. An important thing to note about the input for the problem is that a pair such as `[a, b]` represents that the course `b` needs to be taken in order to do the course `a`. This implies an edge of the form `b ➔ a`. Please take note of this when implementing the algorithm.

3. For each of the nodes in our graph, we will run a depth first search in case that node was not already visited in some other node's DFS traversal.

4. Suppose we are executing the depth first search for a node `N`. We will recursively traverse all of the neighbors of node `N` which have not been processed before.

5. Once the processing of all the neighbors is done, we will add the node `N` to the stack. We are making use of a stack to simulate the ordering we need. When we add the node `N` to the stack, all the nodes that require the node `N` as a prerequisites (among others) will already be in the stack.

6. Once all the nodes have been processed, we will simply return the nodes as they are present in the stack from top to bottom.

#### Implementation 
```java
class Solution {
  static int WHITE = 1;
  static int GRAY = 2;
  static int BLACK = 3;

  boolean isPossible;
  Map<Integer, Integer> color;
  Map<Integer, List<Integer>> adjList;
  List<Integer> topologicalOrder;

  private void init(int numCourses) {
    this.isPossible = true;
    this.color = new HashMap<Integer, Integer>();
    this.adjList = new HashMap<Integer, List<Integer>>();
    this.topologicalOrder = new ArrayList<Integer>();

    // By default all vertces are WHITE
    for (int i = 0; i < numCourses; i++) {
      this.color.put(i, WHITE);
    }
  }

  private void dfs(int node) {

    // Don't recurse further if we found a cycle already
    if (!this.isPossible) {
      return;
    }

    // Start the recursion
    this.color.put(node, GRAY);

    // Traverse on neighboring vertices
    for (Integer neighbor : this.adjList.getOrDefault(node, new ArrayList<Integer>())) {
      if (this.color.get(neighbor) == WHITE) {
        this.dfs(neighbor);
      } else if (this.color.get(neighbor) == GRAY) {
        // An edge to a GRAY vertex represents a cycle
        this.isPossible = false;
      }
    }

    // Recursion ends. We mark it as black
    this.color.put(node, BLACK);
    this.topologicalOrder.add(node);
  }

  public int[] findOrder(int numCourses, int[][] prerequisites) {

    this.init(numCourses);

    // Create the adjacency list representation of the graph
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> lst = adjList.getOrDefault(src, new ArrayList<Integer>());
      lst.add(dest);
      adjList.put(src, lst);
    }

    // If the node is unprocessed, then call dfs on it.
    for (int i = 0; i < numCourses; i++) {
      if (this.color.get(i) == WHITE) {
        this.dfs(i);
      }
    }

    int[] order;
    if (this.isPossible) {
      order = new int[numCourses];
      for (int i = 0; i < numCourses; i++) {
        order[i] = this.topologicalOrder.get(numCourses - i - 1);
      }
    } else {
      order = new int[0];
    }

    return order;
  }
}
```
#### Complexity Analysis

**Time Complexity:** O(V+E) where V represents the number of vertices and E represents the number of edges. Essentially we iterate through each node and each vertex in the graph once and only once.

**Space Complexity:** O(V+E).

We use the adjacency list to represent our graph initially. The space occupied is defined by the number of edges because for each node as the key, we have all its adjacent nodes in the form of a list as the value. Hence, O(E)

Additionally, we apply recursion in our algorithm, which in worst case will incur O(E) extra space in the function call stack.

To sum up, the overall space complexity is O(V+E).

### solution 2 : Using Node Indegree

**Algorithm**

1. Initialize a queue, `Q` to keep a track of all the nodes in the graph with 0 in-degree.

2. Iterate over all the edges in the input and create an adjacency list and also a map of node v/s in-degree.

3. Add all the nodes with 0 in-degree to `Q`.

4. The following steps are to be done until the `Q` becomes empty.
   * Pop a node from the `Q`. Let's call this node, `N`.

   * For all the neighbors of this node, `N`, reduce their in-degree by 1. If any of the nodes' in-degree reaches 0, add it to the `Q`.

   * Add the node `N` to the list maintaining topologically sorted order.

   * Continue from step 4.1.

#### Implementation
```java
class Solution {
  public int[] findOrder(int numCourses, int[][] prerequisites) {

    boolean isPossible = true;
    Map<Integer, List<Integer>> adjList = new HashMap<Integer, List<Integer>>();
    int[] indegree = new int[numCourses];
    int[] topologicalOrder = new int[numCourses];

    // Create the adjacency list representation of the graph
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> lst = adjList.getOrDefault(src, new ArrayList<Integer>());
      lst.add(dest);
      adjList.put(src, lst);

      // Record in-degree of each vertex
      indegree[dest] += 1;
    }

    // Add all vertices with 0 in-degree to the queue
    Queue<Integer> q = new LinkedList<Integer>();
    for (int i = 0; i < numCourses; i++) {
      if (indegree[i] == 0) {
        q.add(i);
      }
    }

    int i = 0;
    // Process until the Q becomes empty
    while (!q.isEmpty()) {
      int node = q.remove();
      topologicalOrder[i++] = node;

      // Reduce the in-degree of each neighbor by 1
      if (adjList.containsKey(node)) {
        for (Integer neighbor : adjList.get(node)) {
          indegree[neighbor]--;

          // If in-degree of a neighbor becomes 0, add it to the Q
          if (indegree[neighbor] == 0) {
            q.add(neighbor);
          }
        }
      }
    }

    // Check to see if topological sort is possible or not.
    if (i == numCourses) {
      return topologicalOrder;
    }

    return new int[0];
  }
}
```

#### Complexity Analysis

**Time Complexity:** O(V+E) where V represents the number of vertices and E represents the number of edges. We pop each node exactly once from the zero in-degree queue and that gives us V. Also, for each vertex, we iterate over its adjacency list and in totality, we iterate over all the edges in the graph which gives us E. Hence, O(V+E)

**Space Complexity:** O(V+E). We use an intermediate queue data structure to keep all the nodes with 0 in-degree. In the worst case, there won't be any prerequisite relationship and the queue will contain all the vertices initially since all of them will have 0 in-degree. That gives us O(V). Additionally, we also use the adjacency list to represent our graph initially. The space occupied is defined by the number of edges because for each node as the key, we have all its adjacent nodes in the form of a list as the value. Hence, O(E). So, the overall space complexity is O(V+E).

### Solution 3 : 

```java
public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (numCourses <= 0) {
			return null;
		}
		int[] res = new int[numCourses];
		int index = 0;
		if (prerequisites.length == 0 || prerequisites[0].length == 0) {
			while (index < numCourses) {
				res[index] = index++;
			}
			return res;
		}
        int[] course = new int[numCourses];
		Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
		for (int i = 0; i < prerequisites.length; i++) {
			int val = prerequisites[i][0];
			int key = prerequisites[i][1];
			if (!map.containsKey(key)) {
				map.put(key, new ArrayList<Integer>());
			}
			map.get(key).add(val);
			course[val]++;
		}
		Queue<Integer> queue = new LinkedList<Integer>();
		for (int i = 0; i < numCourses; i++) {
			if (course[i] == 0) {
				queue.add(i);
				res[index++] = i;
			}
		}
		while (!queue.isEmpty()) {
			int cur = queue.poll();
			if (map.get(cur) != null) {
				for (int temp : map.get(cur)) {
					course[temp]--;
					if (course[temp] == 0) {
						queue.offer(temp);
						res[index++] = temp;
					}
				}
			}
		}
		for (int i = 0; i < numCourses; i++) {
			if (course[i] != 0) {
				return new int[0];
			}
		}
		return res;
    }
}
```

---














