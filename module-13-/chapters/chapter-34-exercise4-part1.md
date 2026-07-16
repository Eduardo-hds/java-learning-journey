# Chapter 34 — Exercise 4: Task Queue System (Part 1)

Until now, we learned collections that represent:

* **List** → ordered group of elements.
* **Set** → unique elements.
* **Map** → key/value relationships.

Now we introduce another important concept:

> Processing elements in a specific order.

This is where `Queue` exists.

---

# Exercise Objective

Create a task processing system.

The system should:

* Add tasks to a queue.
* Process tasks in FIFO order.
* Remove processed tasks.
* Display pending tasks.

---

# Real-World Examples of Queues

Queues exist everywhere.

Examples:

## Printer system

```text
Document 1
Document 2
Document 3
```

The first document sent prints first.

---

## Customer service

```text
Customer A
Customer B
Customer C
```

First customer waits first.

---

## Background jobs

```text
Task A
Task B
Task C
```

Processed in arrival order.

---

# Queue Concept

Queue follows:

```text
FIFO
```

Meaning:

> First In, First Out.

---

Example:

Add:

```text id="k9m3x7"
A
B
C
```

Queue:

```text id="p5q8m2"
Front
 |
 v

[A][B][C]

        ^
       End
```

Remove:

```text id="x7m4q9"
A
```

Remaining:

```text id="z3m8p1"
[B][C]
```

---

# Queue Interface

Java provides:

```java id="n4q7m2"
Queue<E>
```

It extends:

```text id="s8m3x5"
Collection
```

Hierarchy:

```text
Collection

    |
    v

 Queue
```

---

# Main Queue Operations

A Queue has specific methods.

---

# Adding Elements

## add()

```java id="w5m8q3"
queue.add(element);
```

Adds element.

If it fails:

Throws exception.

---

## offer()

```java id="m7x2q9"
queue.offer(element);
```

Adds element.

Returns:

```text id="c5q8m1"
true / false
```

---

# Removing Elements

## remove()

```java id="h3m9x7"
queue.remove();
```

Removes first element.

If empty:

Throws exception.

---

## poll()

```java id="v8q2m5"
queue.poll();
```

Removes first element.

If empty:

Returns:

```text id="x4m7q9"
null
```

---

# Viewing First Element

## element()

```java id="p6m3x8"
queue.element();
```

Returns first element.

Empty:

Throws exception.

---

## peek()

```java id="y5q9m2"
queue.peek();
```

Returns first element.

Empty:

Returns:

```text id="k8m4x3"
null
```

---

# Method Comparison

| Operation | Exception version | Safe version |
| --------- | ----------------- | ------------ |
| Add       | add()             | offer()      |
| Remove    | remove()          | poll()       |
| View      | element()         | peek()       |

---

# Choosing Safe Methods

Most applications prefer:

```java id="q7m4x9"
offer()
poll()
peek()
```

because they handle empty states better.

---

# Queue Implementations

Java has several Queue implementations.

Main ones:

```text id="m2x8q5"
Queue

 |
 +-- LinkedList

 |
 +-- PriorityQueue

 |
 +-- ArrayDeque
```

---

For this exercise we start with:

```java id="z6m3q8"
LinkedList
```

because it demonstrates FIFO clearly.

---

# Project Structure

Add:

```text id="n8q3m5"
src/
│
├── Main.java
│
├── model/
│   └── Task.java
│
├── service/
│   └── TaskService.java
│
└── util/
```

---

# Step 1 — Create Task Model

Location:

```text id="x5m9q2"
model/Task.java
```

---

Attributes:

```java id="v3m8q1"
public class Task {

    private int id;
    private String description;

}
```

---

Example:

```text id="p8q4m6"
Task

ID: 1
Description: Send email
```

---

# Step 2 — Constructor

```java id="r7m2x9"
public Task(
        int id,
        String description){

    this.id = id;
    this.description = description;

}
```

---

# Step 3 — Getters

```java id="d5q8m3"
public int getId(){

    return id;

}
```

---

```java id="g9m4x2"
public String getDescription(){

    return description;

}
```

---

# Step 4 — toString()

Add:

```java id="f6m8q1"
@Override
public String toString(){

    return "Task{" +
            "id=" + id +
            ", description='" +
            description + '\'' +
            '}';

}
```

---

# Step 5 — Create TaskService

Location:

```text id="h7m3x9"
service/TaskService.java
```

---

Create Queue:

```java id="q4m8p2"
private Queue<Task> tasks =
        new LinkedList<>();
```

---

# Why Queue Interface?

Same principle:

Prefer:

```java id="v5x9m3"
Queue<Task>
```

not:

```java id="c8m2q7"
LinkedList<Task>
```

---

Because we need:

```text id="k3m7q5"
Queue behavior
```

not linked list details.

---

# Step 6 — Add Task

Method:

```java id="n6q2x8"
public void addTask(Task task){

    tasks.offer(task);

}
```

---

Example:

```java id="w9m4p3"
Task t1 =
    new Task(
        1,
        "Send email"
    );


addTask(t1);
```

---

Queue:

```text id="b7x3m9"
[Send email]
```

---

Add more:

```text id="m5q8v2"
[Send email][Backup files][Generate report]
```

---

# Step 7 — Process Task

Method:

```java id="z8m4q1"
public Task processTask(){

    return tasks.poll();

}
```

---

Example:

Queue:

```text id="p3x7m5"
[A][B][C]
```

Call:

```java id="h9q2m6"
processTask();
```

Returns:

```text id="r4m8x1"
A
```

Queue becomes:

```text id="v6q3p9"
[B][C]
```

---

# Step 8 — Display Pending Tasks

Method:

```java id="t5m9x2"
public void listTasks(){

    for(Task task : tasks){

        System.out.println(task);

    }

}
```

---

# Complete Flow

```text id="w7m3q8"
Main

 |
 v

TaskService

 |
 v

Queue<Task>

 |
 v

Task objects
```

---

# Queue Complexity

Using LinkedList:

| Operation | Complexity |
| --------- | ---------- |
| offer()   | O(1)       |
| poll()    | O(1)       |
| peek()    | O(1)       |

---

# Why Queue Is Efficient

Because we only interact with:

```text id="q8m4x3"
Beginning
and
End
```

We do not search through elements.

---

# Exercise Task

Create:

### Task.java

Implement:

* id.
* description.
* constructor.
* getters.
* toString().

---

### TaskService.java

Implement:

* Queue storage.
* addTask().
* processTask().
* listTasks().

---

Test:

Add:

```text id="x6m2q9"
Task 1 - Backup
Task 2 - Email
Task 3 - Report
```

Process tasks.

Expected:

```text id="m3q8v5"
Backup
Email
Report
```

---

# ✔️ Next Step

In **Chapter 35 — Exercise 4: Task Queue System (Part 2)** we will expand this system:

* Introduce `PriorityQueue`.
* Understand priority ordering.
* Compare FIFO Queue vs priority-based processing.
* Create tasks with different priorities.
