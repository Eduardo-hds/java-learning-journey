# Chapter 11 — Queue Interface

Until now, we studied collections focused on storing data:

* `List` → ordered sequence of elements.
* `Set` → unique elements.

Now we will study a collection designed around **processing order**:

```java
Queue
```

A queue represents a line of elements waiting to be processed.

Examples from real systems:

* Printer jobs.
* Customer service requests.
* Background tasks.
* Message processing.
* Ticket systems.

The central idea:

> The first element that enters is usually the first element that leaves.

This is called:

```text
FIFO
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What a `Queue` is.
* Why queues exist.
* The FIFO principle.
* How queues differ from Lists.
* Main Queue operations.
* Internal behavior.
* Time complexity.
* When to use Queue.

---

# What is a Queue?

A `Queue` is a collection designed for processing elements in a specific order.

The most common behavior is:

```text
FIFO

First In
First Out
```

Example:

People waiting in line:

```text
Front

Alice
Bob
Charlie

Back
```

The first person served:

```text
Alice
```

---

# Why Does Queue Exist?

Imagine a system receiving tasks:

```text
Task A arrives
Task B arrives
Task C arrives
```

The system should process:

```text
Task A
Task B
Task C
```

A normal list could store them:

```java
List<Task> tasks;
```

But the intent is unclear.

A Queue communicates the business rule:

> "These elements are waiting to be processed."

The data structure itself represents the workflow.

---

# Queue in the Collections Hierarchy

The hierarchy:

```text
                Collection
                    |
                Queue
                    |
        ---------------------
        |                   |
 PriorityQueue          Deque
                            |
                       ArrayDeque
```

`Queue` extends:

```java
Collection
```

so it inherits methods like:

* add()
* remove()
* contains()
* size()

---

# Creating a Queue

The common style:

```java
Queue<String> queue = new LinkedList<>();
```

Example:

```java
Queue<String> customers = new LinkedList<>();

customers.add("Alice");
customers.add("Bob");
customers.add("Charlie");
```

Conceptually:

```text
Front

Alice -> Bob -> Charlie

Back
```

---

# Main Queue Operations

A Queue has operations based on two actions:

* Insert element.
* Remove element.

---

# Adding Elements

There are two common methods:

## add()

Example:

```java
queue.add("Alice");
```

Behavior:

Adds the element.

If insertion fails:

```text
Exception
```

may occur.

---

## offer()

Example:

```java
queue.offer("Alice");
```

Behavior:

Attempts to add.

Returns:

```text
true
```

or:

```text
false
```

No exception for normal capacity limitations.

---

# add() vs offer()

Example:

```java
queue.add(task);
```

means:

> "Insert this element. Failure is exceptional."

---

```java
queue.offer(task);
```

means:

> "Try to insert this element."

For many queue implementations:

```java
offer()
```

is preferred.

---

# Removing Elements

Again, two approaches.

---

# remove()

Example:

```java
queue.remove();
```

Removes the head.

If empty:

```text
NoSuchElementException
```

---

# poll()

Example:

```java
queue.poll();
```

Removes and returns the head.

If empty:

```text
null
```

---

# remove() vs poll()

Empty queue:

```java
Queue<String> queue = new LinkedList<>();
```

Using:

```java
queue.remove();
```

Result:

```
Exception
```

Using:

```java
queue.poll();
```

Result:

```
null
```

---

# Checking the First Element

Two methods:

---

## element()

```java
queue.element();
```

Returns first element.

If empty:

```
Exception
```

---

## peek()

```java
queue.peek();
```

Returns first element.

If empty:

```
null
```

---

# Queue Method Comparison

| Operation | Throws Exception | Returns Special Value |
| --------- | ---------------- | --------------------- |
| Insert    | add()            | offer()               |
| Remove    | remove()         | poll()                |
| Inspect   | element()        | peek()                |

---

# Example: Customer Queue

```java
Queue<String> customers = new LinkedList<>();

customers.offer("Carlos");
customers.offer("Ana");
customers.offer("Maria");
```

Queue:

```
Front

Carlos
Ana
Maria

Back
```

Process:

```java
System.out.println(customers.poll());
```

Output:

```
Carlos
```

Remaining:

```
Ana
Maria
```

---

# FIFO Behavior

Let's simulate.

Add:

```text
A
B
C
```

Queue:

```
A -> B -> C
```

Remove:

```
A
```

Remaining:

```
B -> C
```

Remove:

```
B
```

Remaining:

```
C
```

The oldest element always leaves first.

---

# Queue vs List

Many beginners ask:

> "Why not just use ArrayList?"

Let's compare.

---

## List

Represents:

```text
A collection of elements
```

Example:

```java
products.get(10);
```

You care about position.

---

## Queue

Represents:

```text
A waiting line
```

Example:

```java
tasks.poll();
```

You care about processing order.

---

# Comparison

| Feature      | List           | Queue            |
| ------------ | -------------- | ---------------- |
| Index access | Yes            | No               |
| Main purpose | Store data     | Process data     |
| Ordering     | Position based | Processing based |
| Remove first | Depends        | Designed for it  |

---

# Internal Implementation

The `Queue` interface does not define storage.

Different implementations use different structures.

---

## LinkedList Queue

Conceptually:

```
A -> B -> C
```

Adding/removing ends are efficient.

---

## PriorityQueue

Uses:

```
Heap structure
```

Elements leave based on priority.

We will study this next.

---

## ArrayDeque

Uses:

```
Resizable array
```

Efficient for both ends.

---

# Time Complexity Preview

Depends on implementation.

For a linked queue:

| Operation | Complexity |
| --------- | ---------- |
| offer     | O(1)       |
| poll      | O(1)       |
| peek      | O(1)       |

---

# Memory Considerations

A queue requires additional structure to maintain order.

For a linked implementation:

Each element needs references:

```
Previous
Data
Next
```

Similar to linked structures.

---

# Advantages of Queue

## 1. Represents Real Processes

Examples:

* tasks,
* requests,
* messages.

---

## 2. Natural FIFO Handling

No manual index management.

---

## 3. Clear Intent

The code explains the business rule.

Example:

```java
queue.poll();
```

means:

> Process the next waiting item.

---

# Disadvantages of Queue

## 1. No Random Access

Cannot do:

```java
queue.get(5);
```

---

## 2. Wrong Choice for General Storage

If you only need to store objects:

Use:

```java
List
```

---

# When Should You Use Queue?

Use Queue when:

✅ Elements wait to be processed.

Examples:

* task systems,
* customer queues,
* print queues,
* job scheduling.

---

# When Should You NOT Use Queue?

Avoid Queue when:

❌ You need index access.

Use:

```java
List
```

---

❌ You need unique elements.

Use:

```java
Set
```

---

❌ You need key-value relationships.

Use:

```java
Map
```

---

# Practical Example — Task Processing

Imagine:

```text
New tasks arrive:

Backup
Email
Report
```

Queue:

```java
Queue<Task> tasks = new LinkedList<>();
```

Adding:

```java
tasks.offer(backup);
tasks.offer(email);
tasks.offer(report);
```

Processing:

```java
Task task = tasks.poll();
```

The oldest task is always processed first.

---

# Common Mistakes

## Mistake 1 — Treating Queue like List

Wrong:

```java
queue.get(0);
```

Queues do not expose indexes.

---

## Mistake 2 — Forgetting FIFO

The order matters.

Adding:

```
A
B
C
```

does not mean:

```
C
B
A
```

---

## Mistake 3 — Using LinkedList automatically

`LinkedList` works as a Queue, but later we will see:

```java
ArrayDeque
```

is often a better choice for queue behavior.

---

# Chapter Summary

In this chapter, you learned:

* `Queue` represents a waiting line of elements.
* The default behavior is FIFO.
* Main operations are:

  * `offer()`
  * `poll()`
  * `peek()`
* Queues represent processing workflows.
* They are different from Lists because the focus is not storage, but order of processing.

The key idea:

> A Queue is not just a collection of data; it is a model of a process.

---

# ✔️ Next Step

In **Chapter 12 — PriorityQueue**, we will study a special type of queue where FIFO is replaced by priority. You will learn how Java processes the most important elements first, how heaps work conceptually, and when priority-based processing is useful.
