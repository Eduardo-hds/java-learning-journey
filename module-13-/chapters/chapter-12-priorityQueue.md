# Chapter 12 — PriorityQueue

In the previous chapter, we learned that a normal `Queue` follows:

```text
FIFO

First In
First Out
```

However, many real-world systems do not process tasks strictly by arrival time.

Examples:

* Emergency systems.
* Operating system scheduling.
* Customer support priority levels.
* Game event processing.
* Network packet handling.

Sometimes the rule is:

> "Process the most important element first."

This is where:

```java
PriorityQueue
```

is used.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `PriorityQueue` is.
* Why it exists.
* How it differs from normal queues.
* How priorities are defined.
* Internal heap structure.
* Comparable and Comparator usage.
* Performance characteristics.
* When to use and avoid it.

---

# What is PriorityQueue?

`PriorityQueue` is a queue where elements are removed according to their priority instead of insertion order.

Example:

Normal Queue:

```text
Added:

A
B
C

Removed:

A
B
C
```

---

PriorityQueue:

```text
Added:

Low priority
High priority
Medium priority

Removed:

High priority
Medium priority
Low priority
```

---

# Why Does PriorityQueue Exist?

Imagine a hospital emergency system.

Patients arrive:

```text
Patient A - headache
Patient B - critical condition
Patient C - broken arm
```

A normal queue:

```text
A
B
C
```

would process the headache first.

That is incorrect.

A priority queue processes:

```text
B
C
A
```

because priority determines the order.

---

# Queue vs PriorityQueue

| Feature            | Queue         | PriorityQueue  |
| ------------------ | ------------- | -------------- |
| Ordering rule      | Arrival order | Priority       |
| Behavior           | FIFO          | Priority-based |
| Example            | Line at store | Emergency room |
| Internal structure | Depends       | Heap           |

---

# Creating a PriorityQueue

Example:

```java id="z8fw4c"
Queue<Integer> numbers = new PriorityQueue<>();

numbers.add(50);
numbers.add(10);
numbers.add(30);
```

Removing:

```java id="z9t8mr"
System.out.println(numbers.poll());
```

Output:

```text
10
```

Why?

Because the default priority is:

```text
natural ordering
```

Smallest values have highest priority.

---

# Important: PriorityQueue Does NOT Sort Everything

A common misconception:

> "PriorityQueue keeps all elements sorted."

Incorrect.

Example:

```java
Queue<Integer> numbers = new PriorityQueue<>();

numbers.add(50);
numbers.add(10);
numbers.add(30);
numbers.add(5);
```

Internal structure is not:

```text
5
10
30
50
```

Instead, it maintains only enough organization to guarantee:

> The next removed element has the highest priority.

Only the head is guaranteed.

---

# Internal Implementation

`PriorityQueue` uses a:

```text
Heap
```

Specifically:

```text
Binary Heap
```

Conceptually:

```text
        10

       /  \

     30    20

    /

  50
```

The smallest element is always at the root.

---

# What is a Heap?

A heap is a tree structure with a special rule.

For a **min-heap**:

Parent:

```text
smaller than children
```

Example:

```text
        5

      /   \

    10     20

   /

 30
```

The root is always the smallest value.

---

# Adding Elements

Example:

```java
queue.offer(15);
```

Conceptually:

1. Insert element.
2. Move it upward if necessary.

This process is called:

```text
heapify up
```

---

# Removing Elements

Example:

```java
queue.poll();
```

Steps:

1. Remove root.
2. Move another element to the top.
3. Reorganize heap.

Called:

```text
heapify down
```

---

# Defining Priority

There are two ways.

---

# 1. Natural Ordering (Comparable)

Example:

```java
PriorityQueue<Integer> numbers =
        new PriorityQueue<>();
```

Integers already know their ordering.

Smallest:

```text
highest priority
```

---

For custom objects:

```java
class Task implements Comparable<Task>{

}
```

Implement:

```java
compareTo()
```

Example:

```java
@Override
public int compareTo(Task other){

    return this.priority - other.priority;

}
```

---

# 2. Comparator

Usually more flexible.

Example:

Task:

```java
class Task {

    String name;
    int priority;

}
```

Create:

```java
Comparator<Task> comparator =
    (t1, t2) ->
    Integer.compare(
        t1.getPriority(),
        t2.getPriority()
    );
```

Use:

```java
Queue<Task> tasks =
    new PriorityQueue<>(comparator);
```

---

# Example — Task Scheduler

Tasks:

```text
Backup       priority 3
Email        priority 1
Security     priority 5
```

Priority rule:

Higher number = more important.

Comparator:

```java
(t1,t2) ->
Integer.compare(
    t2.priority,
    t1.priority
)
```

Processing:

```text
Security
Backup
Email
```

---

# Basic Operations

## offer()

Adds element:

```java
queue.offer(task);
```

Complexity:

```text
O(log n)
```

---

## poll()

Removes highest priority element:

```java
queue.poll();
```

Complexity:

```text
O(log n)
```

---

## peek()

Views first element:

```java
queue.peek();
```

Complexity:

```text
O(1)
```

---

# Time Complexity

| Operation                | Complexity |
| ------------------------ | ---------- |
| Insert                   | O(log n)   |
| Remove                   | O(log n)   |
| Peek                     | O(1)       |
| Search arbitrary element | O(n)       |

---

# Why Search Is O(n)?

A heap is not fully sorted.

Example:

```text
        5

      /   \

    20     10

   /  \

 30   40
```

Finding:

```text
40
```

requires searching.

---

# Memory Considerations

Internally, `PriorityQueue` uses a dynamic array representing the heap.

Conceptually:

```text
Array:

[5][10][20][30]
```

The tree relationship is calculated using indexes.

Advantages:

* Less memory than linked structures.
* Good CPU cache behavior.

---

# Advantages of PriorityQueue

## 1. Efficient Priority Processing

Best for:

* scheduling,
* ranking,
* urgent tasks.

---

## 2. Automatic Priority Management

No need to manually search for the next item.

---

## 3. Efficient Head Operations

The most important element is always available.

---

# Disadvantages of PriorityQueue

## 1. Not FIFO

Arrival order is ignored.

---

## 2. No Random Access

Cannot:

```java
queue.get(5);
```

---

## 3. Not Fully Sorted

Only the next element is guaranteed.

---

# When Should You Use PriorityQueue?

Use it when:

✅ Processing depends on importance.

Examples:

* task scheduler,
* emergency system,
* game events,
* job processing.

---

# When Should You NOT Use PriorityQueue?

Avoid it when:

❌ You need FIFO.

Use:

```java
Queue
```

---

❌ You need all elements always sorted.

Use:

```java
TreeSet
```

or sort a List.

---

❌ You need indexed access.

Use:

```java
ArrayList
```

---

# Practical Example — Game Event System

Imagine a game:

Events:

```text
Enemy attack     priority 10
Player message   priority 2
Animation        priority 1
```

The game should process:

```text
Enemy attack
Player message
Animation
```

A PriorityQueue naturally models this.

---

# Common Mistakes

## Mistake 1 — Thinking it keeps sorted output

Wrong:

```text
PriorityQueue = sorted collection
```

Correct:

```text
PriorityQueue = priority access collection
```

---

## Mistake 2 — Forgetting Comparator direction

Example:

```java
Integer.compare(a,b)
```

and:

```java
Integer.compare(b,a)
```

create different priorities.

---

## Mistake 3 — Using it as a normal List

It is not designed for:

```java
get(index)
```

---

# Chapter Summary

In this chapter, you learned:

* `PriorityQueue` processes elements by priority.
* It uses a heap internally.
* The head element is always the highest priority.
* Ordering depends on `Comparable` or `Comparator`.
* Insert/remove operations are O(log n).
* It is ideal for scheduling and prioritization problems.

The key idea:

> Queue answers "who arrived first?" while PriorityQueue answers "who is most important?"

---

# ✔️ Next Step

In **Chapter 13 — Deque Interface**, we will study double-ended queues. You will learn how Java supports both queue and stack behavior, why `Deque` replaced many old stack patterns, and how `ArrayDeque` provides a highly efficient implementation.
