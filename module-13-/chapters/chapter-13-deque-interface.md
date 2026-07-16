# Chapter 13 — Deque Interface

Until now, we studied queues where elements normally enter from one side and leave from the other:

```text
Front → A → B → C → Back
```

This is the classic FIFO model.

However, some problems require more flexibility:

* Add elements at both ends.
* Remove elements from both ends.
* Use the structure as a queue.
* Use the structure as a stack.

Java provides:

```java
Deque
```

which means:

```text
Double Ended Queue
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `Deque` is.
* Why it exists.
* How it differs from Queue.
* How it can behave like a Queue.
* How it can behave like a Stack.
* Internal implementation concept.
* `ArrayDeque`.
* Performance characteristics.
* When to use Deque.

---

# What is Deque?

A `Deque` is a queue where insertion and removal can happen at **both ends**.

Example:

```text
Front

A <-> B <-> C

Back
```

You can:

Add:

```text
Front
or
Back
```

Remove:

```text
Front
or
Back
```

---

# Why Does Deque Exist?

A normal queue:

```text
A -> B -> C
```

allows:

```text
add at back
remove at front
```

But many algorithms need both directions.

Examples:

* Browser history.
* Undo/redo systems.
* Sliding window algorithms.
* Task processing.
* Stack operations.

A Deque gives both behaviors.

---

# Deque in the Collections Hierarchy

The hierarchy:

```text
              Collection
                  |
              Queue
                  |
              Deque
                  |
             ArrayDeque
```

`Deque` extends:

```java
Queue
```

and adds operations for both ends.

---

# Creating a Deque

Common implementation:

```java
Deque<String> deque = new ArrayDeque<>();
```

Example:

```java
Deque<String> names = new ArrayDeque<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Conceptually:

```text
Front

Alice <-> Bob <-> Charlie

Back
```

---

# Deque as a Queue

A Deque can behave exactly like a normal queue.

FIFO:

```text
First In
First Out
```

Example:

```java
Deque<String> queue = new ArrayDeque<>();

queue.offer("A");
queue.offer("B");
queue.offer("C");
```

Structure:

```text
A -> B -> C
```

Remove:

```java
queue.poll();
```

Result:

```text
A
```

Remaining:

```text
B -> C
```

---

# Queue Methods in Deque

Deque supports Queue methods:

| Queue Operation | Deque Method |
| --------------- | ------------ |
| Add             | offer()      |
| Remove          | poll()       |
| View            | peek()       |

Example:

```java
deque.offer("Java");
deque.poll();
deque.peek();
```

---

# Adding at the Front

Now we use Deque-specific operations.

---

## addFirst()

Example:

```java
deque.addFirst("A");
```

Before:

```text
B -> C
```

After:

```text
A -> B -> C
```

---

## offerFirst()

Safer version:

```java
deque.offerFirst("A");
```

---

# Adding at the Back

---

## addLast()

Example:

```java
deque.addLast("C");
```

Result:

```text
A -> B -> C
```

---

## offerLast()

```java
deque.offerLast("C");
```

---

# Removing from the Front

---

## removeFirst()

```java
deque.removeFirst();
```

---

## pollFirst()

```java
deque.pollFirst();
```

Returns:

```text
null
```

if empty.

---

# Removing from the Back

---

## removeLast()

```java
deque.removeLast();
```

---

## pollLast()

```java
deque.pollLast();
```

---

# Complete Deque Example

```java
Deque<Integer> numbers = new ArrayDeque<>();

numbers.addFirst(20);
numbers.addLast(30);
numbers.addFirst(10);
```

Result:

```text
10 -> 20 -> 30
```

Remove:

```java
numbers.removeLast();
```

Result:

```text
10 -> 20
```

---

# Deque as a Stack

Before Java collections improvements, developers commonly used:

```java
Stack
```

But today:

```java
Deque
```

is preferred.

Why?

Because it is faster and more flexible.

---

# Stack Concept

A stack follows:

```text
LIFO

Last In
First Out
```

Example:

A stack of plates:

```text
Top

Plate C
Plate B
Plate A

Bottom
```

The last plate added is the first removed.

---

# Stack Operations Using Deque

Push:

```java
deque.push(element);
```

Equivalent:

```java
addFirst()
```

---

Pop:

```java
deque.pop();
```

Equivalent:

```java
removeFirst()
```

---

Peek:

```java
deque.peek();
```

---

# Stack Example

```java
Deque<String> stack = new ArrayDeque<>();

stack.push("A");
stack.push("B");
stack.push("C");
```

Structure:

```text
Top

C
B
A
```

Remove:

```java
stack.pop();
```

Returns:

```text
C
```

---

# Queue vs Stack Behavior

Same structure:

```text
Deque
```

Different usage.

---

## Queue

Insert:

```text
Back
```

Remove:

```text
Front
```

Behavior:

```text
FIFO
```

---

## Stack

Insert:

```text
Front
```

Remove:

```text
Front
```

Behavior:

```text
LIFO
```

---

# ArrayDeque Internal Structure

`ArrayDeque` uses:

```text
Resizable circular array
```

Conceptually:

```text
[ ][ ][A][B][C][ ][ ]
```

It keeps track of:

* first position,
* last position.

---

# Why Circular Array?

Imagine:

```text
[ ][ ][A][B][C]
```

Remove A:

```text
[ ][ ][ ][B][C]
```

Instead of shifting everything:

```text
B C
```

Java moves the internal pointer.

This makes operations efficient.

---

# ArrayDeque vs LinkedList

Both can implement Deque.

But they behave differently.

---

# LinkedList

Internal:

```text
Node <-> Node <-> Node
```

Each element stores:

* value,
* previous reference,
* next reference.

---

# ArrayDeque

Internal:

```text
Array
```

Advantages:

* Less memory.
* Better CPU cache usage.
* Usually faster.

---

# Comparison

| Feature           | ArrayDeque    | LinkedList         |
| ----------------- | ------------- | ------------------ |
| Structure         | Dynamic array | Doubly linked list |
| Memory            | Lower         | Higher             |
| Cache performance | Better        | Worse              |
| Queue operations  | Fast          | Fast               |
| Stack operations  | Fast          | Fast               |

---

# Time Complexity

For `ArrayDeque`:

| Operation   | Complexity |
| ----------- | ---------- |
| addFirst    | O(1)       |
| addLast     | O(1)       |
| removeFirst | O(1)       |
| removeLast  | O(1)       |
| peek        | O(1)       |

Occasional resizing can happen, but amortized performance remains excellent.

---

# Memory Considerations

Compared with LinkedList:

ArrayDeque:

```text
[A][B][C]
```

Only stores elements.

LinkedList:

```text
Node
 |
Value
Previous
Next
```

More memory overhead.

---

# Advantages of Deque

## 1. Very Flexible

Can act as:

* Queue.
* Stack.

---

## 2. Efficient Operations

Both ends are optimized.

---

## 3. Modern Replacement for Stack

Preferred over:

```java
Stack
```

in most cases.

---

# Disadvantages of Deque

## 1. No Random Access

Cannot:

```java
deque.get(5);
```

---

## 2. Not Designed for Searching

Searching is:

```text
O(n)
```

---

# When Should You Use Deque?

Use when:

✅ You need insertion/removal from both ends.

Examples:

* undo history,
* browser navigation,
* stack algorithms,
* queue processing.

---

# When Should You NOT Use Deque?

Avoid when:

❌ You need indexes.

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

# Practical Example — Browser History

Imagine:

```text
Previous pages:

Google
YouTube
GitHub
```

Going back removes from the end:

```java
history.removeLast();
```

Going forward adds:

```java
history.addLast(page);
```

Deque naturally represents this behavior.

---

# Common Mistakes

## Mistake 1 — Using Stack class

Old:

```java
Stack<String> stack;
```

Modern:

```java
Deque<String> stack =
    new ArrayDeque<>();
```

---

## Mistake 2 — Thinking Deque sorts elements

It does not.

It only controls insertion/removal positions.

---

## Mistake 3 — Using LinkedList automatically

Although valid:

```java
Deque<String> deque =
    new LinkedList<>();
```

Usually:

```java
ArrayDeque
```

is the preferred implementation.

---

# Chapter Summary

You learned:

* `Deque` means double-ended queue.
* It supports operations at both ends.
* It can behave as:

  * Queue (FIFO)
  * Stack (LIFO)
* `ArrayDeque` is the preferred general implementation.
* It provides O(1) operations at both ends.
* It is usually better than `LinkedList` for queue and stack behavior.

The key idea:

> Deque is the flexible bridge between Queue and Stack.

---

# ✔️ Next Step

In **Chapter 14 — Comparing Queue, PriorityQueue, and Deque**, we will consolidate the queue family, compare their internal behaviors, performance, and decide which one should be chosen for different real-world problems.
