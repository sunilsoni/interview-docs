---
layout: default
title: Queue 
parent: Data Structures

---

# Queue
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

## Implement Queue using Stacks

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

- void push(int x) Pushes element x to the back of the queue.
- int pop() Removes the element from the front of the queue and returns it.
- int peek() Returns the element at the front of the queue.
- boolean empty() Returns true if the queue is empty, false otherwise.

**Example 1:**

Input

```
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
```

Output

```
[null, null, null, 1, 1, false]
```

Explanation

```
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

### Solution 1

I have one input stack, onto which I push the incoming elements, and one output stack, from which I peek/pop. I move elements from input stack to output stack when needed, i.e., when I need to peek/pop but the output stack is empty. When that happens, I move all elements from input to output stack, thereby reversing the order so it's the correct order for peek/pop.

The loop in peek does the moving from input to output stack. Each element only ever gets moved like that once, though, and only after we already spent time pushing it, so the overall amortized cost for each operation is O(1).

####  Implementation

```java
 class MyQueue {
    Stack<Integer> input = new Stack();
    Stack<Integer> output = new Stack();
    
    //Push element x to the back of queue.
    public void push(int x) {
        input.push(x);
    }
    
    //Removes the element from in front of queue.
    public int pop() {
        peek();
       return output.pop();
    }
    
    // Get the front element.
    public int peek() {
        if (output.empty())
            while (!input.empty())
                output.push(input.pop());
        return output.peek();
    }

    // Return whether the queue is empty.
    public boolean empty() {
        return input.empty() && output.empty();
    }

    public static void main(String[] args){
        //Your MyQueue object will be instantiated and called as such:
        MyQueue obj = new MyQueue();
        obj.push(x);
        int param_2 = obj.pop();
        int param_3 = obj.peek();
        boolean param_4 = obj.empty();
    }
}

```

####  Complexity Analysis

**Time Complexity**:

**Space Complexity**:



### Solution 2

Keep 2 stacks, let's call them inbox and outbox.

**Enqueue:**

Push the new element onto inbox

**Dequeue:**

If outbox is empty, refill it by popping each element from inbox and pushing it onto outbox

Pop and return the top element from outbox

Using this method, each element will be in each stack exactly once - meaning each element will be pushed twice and popped twice, giving amortized constant time operations.

####  Implementation

```java
 public class Queue<E>
{

    private Stack<E> inbox = new Stack<E>();
    private Stack<E> outbox = new Stack<E>();

    public void queue(E item) {
        inbox.push(item);
    }

    public E dequeue() {
        if (outbox.isEmpty()) {
            while (!inbox.isEmpty()) {
                outbox.push(inbox.pop());
            }
        }
        return outbox.pop();
    }

}
```


####  Complexity Analysis

**Time Complexity**:

**Space Complexity**:


### One Stack Solution

You can even simulate a queue using only one stack. The second (temporary) stack can be simulated by the call stack of recursive calls to the insert method.

The principle stays the same when inserting a new element into the queue:

- You need to transfer elements from one stack to another temporary stack, to reverse their order.
- Then push the new element to be inserted, onto the temporary stack
- Then transfer the elements back to the original stack
- The new element will be on the bottom of the stack, and the oldest element is on top (first to be popped)

A Queue class using only one Stack, would be as follows:

####  Implementation

```java
 public class SimulatedQueue<E> {
    private java.util.Stack<E> stack = new java.util.Stack<E>();

    public void insert(E elem) {
        if (!stack.empty()) {
            E topElem = stack.pop();
            insert(elem);
            stack.push(topElem);
        }
        else
            stack.push(elem);
    }

    public E remove() {
        return stack.pop();
    }
}
```


---

## More Details: 
1. [How to implement a queue using two stacks?](https://stackoverflow.com/questions/69192/how-to-implement-a-queue-using-two-stacks)