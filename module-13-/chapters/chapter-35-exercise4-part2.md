# Chapter 35 — Exercise 4: Task Queue System (Part 2)

In the previous chapter, we created a basic queue system using:

```java
Queue<Task>
```

with:

```java
LinkedList
```

We learned:

* FIFO behavior.
* `offer()`.
* `poll()`.
* `peek()`.
* Queue operations complexity.

Now we will introduce a different type of queue:

> A queue where order is determined by priority.

This is:

```java
PriorityQueue
```

---

# FIFO vs Priority Queue

The traditional queue:

```text id="c4m8x2"
First In → First Out
```

Example:

Tasks arrive:

```text id="k7q3m9"
Task A
Task B
Task C
```

Processing:

```text id="v5m2x8"
A
B
C
```

---

But real systems often need:

> "Process the most important task first."

Example:

```text id="r8q1m6"
Emergency task
Normal task
Low priority task
```

The emergency task should not wait.

---

# PriorityQueue Concept

A `PriorityQueue` processes elements according to:

```text id="n4m8q2"
priority ordering
```

not insertion order.

---

Example:

Add:

```text id="z7m3x5"
Task A - Priority 3
Task B - Priority 1
Task C - Priority 2
```

Processing:

```text id="p6q9m1"
Task B
Task C
Task A
```

---

# Internal Structure

PriorityQueue is based on:

```text id="x8m2q5"
Heap
```

Usually:

```text id="v3q7m9"
Binary Heap
```

---

High-level idea:

The smallest element stays accessible at the top.

Example:

```text id="w5m8x2"
        1
       / \
      3   5
```

The root is removed first.

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| add()     | O(log n)   |
| poll()    | O(log n)   |
| peek()    | O(1)       |

---

# Why Not O(1) Like LinkedList Queue?

Because PriorityQueue must maintain ordering.

Every insertion may require rearranging the heap.

---

# Updating Our Task Model

Current:

```java id="q5m8x3"
Task

id
description
```

Add:

```text id="m7x3p9"
priority
```

---

# Task.java

New structure:

```java id="b8m4q2"
public class Task {

    private int id;
    private String description;
    private int priority;

}
```

---

# Meaning of Priority

Example:

```text id="h6q9m1"
1 = Highest priority

5 = Lowest priority
```

---

Example:

```text id="t4m8x2"
Task:

Backup database
Priority: 1
```

---

# Constructor

```java id="r7q3m9"
public Task(
        int id,
        String description,
        int priority){

    this.id = id;
    this.description = description;
    this.priority = priority;

}
```

---

# Getter

```java id="p8m2x6"
public int getPriority(){

    return priority;

}
```

---

# toString()

Update:

```java id="w4m9q3"
@Override
public String toString(){

    return "Task{" +
            "id=" + id +
            ", description='" +
            description + '\'' +
            ", priority=" +
            priority +
            '}';

}
```

---

# The Important Question

How does PriorityQueue know the order?

Example:

```java id="z5m3x8"
Task A priority 3

Task B priority 1
```

Java needs to know:

Which one comes first?

---

There are two ways:

1. Comparable.
2. Comparator.

We already saw sorting concepts coming later, but this is our first practical use.

---

# Method 1 — Comparable

The object defines its natural ordering.

---

Task implements:

```java id="x9m4q2"
Comparable<Task>
```

---

Class:

```java id="n7q3m8"
public class Task
        implements Comparable<Task>
```

---

Implement:

```java id="v5m8x1"
@Override
public int compareTo(Task other){

    return Integer.compare(
            this.priority,
            other.priority
    );

}
```

---

Meaning:

Lower number:

```text id="m3q8p5"
higher priority
```

comes first.

---

Comparison:

```text id="j7x2m9"
1 before 3
```

because:

```java id="f4m8q3"
Integer.compare(1,3)
```

returns negative.

---

# Step 2 — Create PriorityQueue

Change service.

New class:

```text id="q6m3x8"
PriorityTaskService.java
```

---

Storage:

```java id="w8m2p5"
private Queue<Task> tasks =
        new PriorityQueue<>();
```

---

Notice:

Still using:

```java id="v3m8q1"
Queue<Task>
```

The implementation changed.

---

# Add Task

```java id="x5m9q2"
public void addTask(Task task){

    tasks.offer(task);

}
```

---

# Process Task

```java id="r4m7x9"
public Task processTask(){

    return tasks.poll();

}
```

---

# Testing

Add:

```java id="s8m2q4"
new Task(
    1,
    "Normal backup",
    3
);


new Task(
    2,
    "Database failure",
    1
);


new Task(
    3,
    "Update report",
    2
);
```

---

Insertion order:

```text id="n6q3m8"
Backup
Failure
Report
```

---

Processing:

```text id="y7m4x2"
Database failure
Update report
Normal backup
```

---

# Important Difference

A normal Queue:

```text id="u5m8q3"
Insertion order
```

---

PriorityQueue:

```text id="p9m2x6"
Priority order
```

---

# Common Mistake

Many developers think:

> PriorityQueue keeps everything sorted.

It does not.

Example:

```java id="z6m3x8"
for(Task task : queue)
```

does not guarantee sorted output.

---

Only removal:

```java id="m4q8x2"
poll()
```

follows priority.

---

# Comparing Queue Types

| Feature            | LinkedList Queue | PriorityQueue |
| ------------------ | ---------------- | ------------- |
| Ordering           | FIFO             | Priority      |
| add()              | O(1)             | O(log n)      |
| remove             | O(1)             | O(log n)      |
| Uses priority      | No               | Yes           |
| Internal structure | Linked nodes     | Heap          |

---

# Real Applications

## LinkedList Queue

Use for:

* Print jobs.
* User requests.
* Messages.

---

## PriorityQueue

Use for:

* Hospital triage.
* CPU scheduling.
* Game AI decisions.
* Emergency processing.

---

# Exercise Task

Implement:

1. Add priority to `Task`.
2. Make `Task` implement `Comparable`.
3. Create `PriorityTaskService`.
4. Add three tasks with priorities:

```text id="k8m4q2"
Task A - priority 3
Task B - priority 1
Task C - priority 2
```

Process them.

Expected:

```text id="p5x9m3"
Task B
Task C
Task A
```

---

# ✔️ Next Step

In **Chapter 36 — Exercise 5: Contact Manager (Part 1)** we will start a new system using:

```java
Map<String, Contact>
```

We will practice:

* HashMap with custom objects.
* Searching by key.
* Updating values.
* Managing contacts efficiently.
