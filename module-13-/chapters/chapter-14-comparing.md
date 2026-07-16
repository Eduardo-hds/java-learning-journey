# Chapter 14 — Comparing Queue, PriorityQueue, and Deque

We have now studied the three main structures used for processing elements:

* `Queue`
* `PriorityQueue`
* `Deque`

Although they all belong to the same family, they solve **different problems**.

The mistake many developers make is thinking:

> "They all store elements, so any one of them works."

That is incorrect.

The correct question is:

> "What rule determines which element should be processed next?"

---

# Learning Objectives

By the end of this chapter, you should be able to:

* Compare Queue, PriorityQueue, and Deque.
* Understand their processing rules.
* Choose the correct structure for a problem.
* Compare internal implementations.
* Understand performance differences.

---

# The Main Decision Question

Ask:

> How should elements leave the collection?

There are three main answers.

---

## 1. First element leaves first

Use:

```java
Queue
```

Rule:

```text
FIFO
```

---

## 2. Most important element leaves first

Use:

```java
PriorityQueue
```

Rule:

```text
Priority
```

---

## 3. Either side can leave first

Use:

```java
Deque
```

Rule:

```text
Front or Back
```

---

# Queue

## Purpose

Represent a waiting line.

Example:

```text
Customer service

Carlos
Ana
Maria
```

Processing:

```text
Carlos
Ana
Maria
```

---

# Internal Structure

Depends on implementation.

Example:

`LinkedList`:

```text
Node <-> Node <-> Node
```

Example:

```text
A -> B -> C
```

---

# Main Operations

Add:

```java
offer()
```

Remove:

```java
poll()
```

Inspect:

```java
peek()
```

---

# Performance

Typical linked queue:

| Operation | Complexity |
| --------- | ---------- |
| offer     | O(1)       |
| poll      | O(1)       |
| peek      | O(1)       |

---

# Best Use Cases

* Customer queues.
* Print jobs.
* Message processing.
* Task pipelines.

---

# PriorityQueue

## Purpose

Process the most important element first.

Example:

Tasks:

```text
Backup       priority 3
Security     priority 10
Email        priority 1
```

Processing:

```text
Security
Backup
Email
```

---

# Internal Structure

Heap:

```text
        1

      /   \

     3     5
```

The root is always the highest priority.

---

# Main Operations

Insert:

```java
offer()
```

Remove:

```java
poll()
```

Inspect:

```java
peek()
```

---

# Performance

| Operation | Complexity |
| --------- | ---------- |
| offer     | O(log n)   |
| poll      | O(log n)   |
| peek      | O(1)       |

---

# Best Use Cases

* Schedulers.
* Emergency systems.
* AI decision systems.
* Event processing.

---

# Deque

## Purpose

Allow operations on both ends.

Example:

```text
Front

A <-> B <-> C

Back
```

---

# Internal Structure

Usually:

```text
ArrayDeque

Dynamic circular array
```

Conceptually:

```text
[A][B][C][ ][ ]
```

---

# Main Operations

Front:

```java
addFirst()
removeFirst()
```

Back:

```java
addLast()
removeLast()
```

---

# Performance

| Operation   | Complexity |
| ----------- | ---------- |
| addFirst    | O(1)       |
| addLast     | O(1)       |
| removeFirst | O(1)       |
| removeLast  | O(1)       |

---

# Best Use Cases

* Stack behavior.
* Undo systems.
* Browser history.
* Double-ended processing.

---

# Complete Comparison

| Feature           | Queue       | PriorityQueue    | Deque               |
| ----------------- | ----------- | ---------------- | ------------------- |
| Main rule         | FIFO        | Priority         | Two ends            |
| Order             | Arrival     | Priority         | Controlled manually |
| Index access      | ❌           | ❌                | ❌                   |
| Internal example  | Linked list | Heap             | Circular array      |
| Add complexity    | O(1)        | O(log n)         | O(1)                |
| Remove complexity | O(1)        | O(log n)         | O(1)                |
| Sorting           | ❌           | Partial priority | ❌                   |

---

# Scenario Analysis

Let's choose the correct collection.

---

# Scenario 1 — Printer Queue

Requirement:

Documents are printed in the order received.

Example:

```text
Report
Invoice
Photo
```

Correct:

```java
Queue<Document>
```

Why?

FIFO.

---

Wrong:

```java
PriorityQueue
```

because urgency is not the rule.

---

# Scenario 2 — Hospital Emergency Room

Requirement:

Critical patients first.

Example:

```text
Low fever
Broken arm
Heart attack
```

Correct:

```java
PriorityQueue<Patient>
```

Why?

Priority determines processing.

---

# Scenario 3 — Undo Feature

Requirement:

Last action must be undone first.

Example:

Actions:

```text
Type A
Type B
Type C
```

Undo:

```text
Type C
Type B
Type A
```

Correct:

```java
Deque<Action>
```

Used as a stack.

---

# Scenario 4 — Browser Navigation

Requirement:

Move backward and forward.

Example:

```text
Google
YouTube
GitHub
```

Need:

* remove last visited page,
* add new pages.

Correct:

```java
Deque<String>
```

---

# Scenario 5 — Game Events

Events:

```text
Enemy attack priority 10
Sound priority 1
Animation priority 2
```

Correct:

```java
PriorityQueue<Event>
```

---

# Queue vs Deque

This comparison is especially important.

---

## Queue

Meaning:

> "A line."

Example:

```text
A -> B -> C
```

You normally remove:

```text
A
```

---

## Deque

Meaning:

> "A line where both ends matter."

Example:

```text
A <-> B <-> C
```

You can remove:

```text
A
```

or:

```text
C
```

---

# PriorityQueue vs TreeSet

A common confusion.

Both involve ordering.

But they have different purposes.

---

## TreeSet

Maintains:

```text
all elements sorted
```

Example:

```text
10
20
30
40
```

---

## PriorityQueue

Maintains:

```text
only the next element priority
```

Example:

```text
10 <- next
30
20
40
```

---

Use:

Sorted collection:

```java
TreeSet
```

Processing system:

```java
PriorityQueue
```

---

# Memory Comparison

Generally:

Less overhead:

```text
ArrayDeque
```

Medium:

```text
Queue implementation
```

More complex:

```text
PriorityQueue
```

because it maintains heap relationships.

---

# Professional Decision Guide

When designing a system:

---

## "Things arrive and leave in order"

Use:

```java
Queue
```

---

## "The most important item goes first"

Use:

```java
PriorityQueue
```

---

## "I need both ends"

Use:

```java
Deque
```

---

# Common Mistakes

## Mistake 1 — Using List as a Queue

Example:

```java
list.remove(0);
```

Problems:

* slower with ArrayList,
* intent is unclear.

Better:

```java
Queue
```

---

## Mistake 2 — Using PriorityQueue for sorting

It is not a sorted collection.

---

## Mistake 3 — Using Queue when priority exists

Example:

Emergency system:

```text
arrival order ≠ processing order
```

---

## Mistake 4 — Using Stack class

Prefer:

```java
Deque
```

---

# Chapter Summary

You learned:

* Queue → FIFO processing.
* PriorityQueue → priority-based processing.
* Deque → operations on both ends.
* Choosing a collection depends on the processing rule.
* Similar collections can have completely different purposes.

The main principle:

> Collections are designed around behavior, not just storage.

---

# ✔️ Next Step

In **Chapter 15 — Map Interface Introduction**, we will begin one of the most important parts of the Collections Framework.

You will learn why `Map` is different from `Collection`, how key-value relationships work, and why structures like `HashMap` are fundamental in almost every Java application.
