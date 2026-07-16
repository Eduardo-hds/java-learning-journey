# Chapter 04 — LinkedList

In the previous chapter, we learned that `ArrayList` is built on top of a dynamic array.

Now we will study a completely different approach.

Instead of storing elements side-by-side in memory, `LinkedList` connects elements through **nodes and references**.

Understanding `LinkedList` is important because it teaches one of the fundamental data structures in computer science: the **linked list**.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `LinkedList` is.
* Why it exists.
* How it works internally.
* The concept of nodes and references.
* How insertion and removal work.
* Performance characteristics.
* Memory differences compared with `ArrayList`.
* When to use and when not to use `LinkedList`.

---

# What is LinkedList?

`LinkedList` is an implementation of the `List` interface that stores elements as a chain of nodes.

Example:

```java
List<String> names = new LinkedList<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Conceptually:

```text
+-------+      +-------+      +-------+
| Alice | ---> |  Bob  | ---> |Charlie|
+-------+      +-------+      +-------+

```

Each element knows where the next element is.

---

# Why Does LinkedList Exist?

`ArrayList` is excellent for:

* accessing elements by index,
* reading data,
* adding elements at the end.

However, it has a weakness:

Insertion and removal in the middle require shifting elements.

Example:

Before:

```text
Index

0     1     2     3

A     B     C     D
```

Insert X at index 1:

```text
0     1     2     3     4

A     X     B     C     D
```

Everything after index 1 must move.

`LinkedList` solves this differently.

---

# Internal Structure of LinkedList

A `LinkedList` is composed of **nodes**.

A node conceptually contains:

```
Node

+---------+
| Data    |
+---------+
| Next    |
+---------+
| Previous|
+---------+

```

Example:

```text
        Node
+----------------+
| Alice          |
| next ----------|------+
| previous       |      |
+----------------+      |
                        ↓

+----------------+
| Bob            |
| next ----------|------+
| previous       |
+----------------+

                        ↓

+----------------+
| Charlie        |
| next = null    |
+----------------+

```

Java's `LinkedList` is a **doubly linked list**.

That means each node knows:

* the next node,
* the previous node.

---

# ArrayList vs LinkedList Memory Model

## ArrayList

Stores references together:

```
Array

+----+----+----+----+
| A  | B  | C  | D  |
+----+----+----+----+

```

The elements are contiguous.

---

## LinkedList

Stores separated nodes:

```
Node        Node        Node

A --------> B --------> C

```

Nodes can exist anywhere in memory.

The references connect them.

---

# Creating a LinkedList

Example:

```java
List<String> names = new LinkedList<>();
```

Notice:

The variable type is still:

```java
List
```

because we program against the interface.

---

# Adding Elements

## Add at the end

```java
names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Result:

```
Alice -> Bob -> Charlie
```

---

## Add at a specific position

```java
names.add(1, "David");
```

Before:

```
Alice -> Bob -> Charlie
```

After:

```
Alice -> David -> Bob -> Charlie
```

Notice what happens:

The nodes are simply reconnected.

No large shifting operation occurs.

---

# How Insertion Works Internally

Suppose we insert:

```
X
```

between:

```
A -> B
```

Before:

```
A --------> B
```

New node:

```
X
```

After:

```
A --------> X --------> B
```

Only references change.

The existing elements do not move.

This is the main advantage of linked structures.

---

# Removing Elements

Example:

```java
names.remove(1);
```

Before:

```
Alice -> Bob -> Charlie
```

Remove Bob:

```
Alice -> Charlie
```

The node is disconnected.

The references are updated.

---

# Accessing Elements

Here is where `LinkedList` becomes weaker.

Example:

```java
names.get(100);
```

With `ArrayList`:

Java calculates the memory position directly.

```
index -> memory location
```

Complexity:

```
O(1)
```

---

With `LinkedList`:

Java must walk through nodes.

Example:

```
Alice
 |
Bob
 |
Charlie
 |
David
 |
...
 |
Target
```

It must follow references one by one.

Complexity:

```
O(n)
```

---

# Time Complexity

Now let's compare operations.

| Operation                           | LinkedList |
| ----------------------------------- | ---------: |
| Access by index                     |       O(n) |
| Search                              |       O(n) |
| Add at beginning                    |       O(1) |
| Add at end                          |       O(1) |
| Remove beginning                    |       O(1) |
| Remove end                          |       O(1) |
| Insert middle (with node reference) |       O(1) |
| Insert middle (by index)            |       O(n) |

---

# Important Detail: Insert by Index

Many beginners hear:

> "LinkedList insertion is O(1)."

This is incomplete.

Example:

```java
list.add(5000, element);
```

Before inserting, Java must find position 5000.

Finding:

```
O(n)
```

Then insertion:

```
O(1)
```

Total:

```
O(n)
```

The advantage exists when you already have the node position.

---

# Memory Considerations

LinkedList requires more memory than ArrayList.

Why?

Every node stores:

* the object reference,
* next reference,
* previous reference.

Example:

ArrayList:

```
[A][B][C]
```

LinkedList:

```
[A,next,previous]

[B,next,previous]

[C,next,previous]

```

More information means more memory overhead.

---

# Advantages of LinkedList

## 1. Efficient Insertions and Removals

Especially at:

* beginning,
* end,
* known positions.

---

## 2. No Large Array Copying

Adding elements does not require resizing or shifting.

---

## 3. Implements Deque

`LinkedList` also implements:

```java
Deque
```

Meaning it can behave like:

* queue,
* stack.

Example:

```java
Deque<String> queue = new LinkedList<>();
```

---

# Disadvantages of LinkedList

## 1. Slow Random Access

This is the biggest disadvantage.

Example:

```java
list.get(5000);
```

Requires traversal.

---

## 2. More Memory Usage

Each node stores additional references.

---

## 3. Poor CPU Cache Performance

Modern processors work efficiently with contiguous memory.

Arrays benefit from this.

Linked structures jump between memory locations.

---

# When Should You Use LinkedList?

Use `LinkedList` when:

✅ You frequently add/remove elements from the beginning.

Example:

```
new messages arrive
old messages removed
```

---

✅ You need queue/deque behavior.

Example:

```java
Deque<Task> tasks = new LinkedList<>();
```

---

✅ You frequently manipulate the ends of the collection.

---

# When Should You NOT Use LinkedList?

Avoid it when:

❌ You frequently access elements by index.

Example:

```java
products.get(1000);
```

---

❌ You mostly read data.

`ArrayList` is usually better.

---

❌ Memory efficiency matters.

LinkedList has higher overhead.

---

# Common Mistakes

## Mistake 1 — Assuming LinkedList is always faster for insertions

Wrong:

> "LinkedList is faster whenever adding."

Reality:

If you need to find the position first:

```
search O(n)
+
insert O(1)

=
O(n)
```

---

## Mistake 2 — Using LinkedList as default

Many developers think:

```
LinkedList = advanced
ArrayList = beginner
```

This is false.

For most applications:

```
ArrayList
```

is the better default.

---

## Mistake 3 — Ignoring memory cost

Thousands or millions of nodes can create significant overhead.

---

# Practical Example — Task Queue

Imagine a task processing system:

```
Receive task

Process oldest task

Remove task

Repeat
```

This is naturally:

```
FIFO
```

A linked structure works well.

Example:

```java
Deque<Task> tasks = new LinkedList<>();

tasks.addLast(task);

Task next = tasks.removeFirst();
```

Later in this module, we will study dedicated queue implementations.

---

# ArrayList vs LinkedList Preview

| Feature            | ArrayList         | LinkedList             |
| ------------------ | ----------------- | ---------------------- |
| Internal structure | Dynamic array     | Doubly linked nodes    |
| Access by index    | O(1)              | O(n)                   |
| Add end            | O(1) average      | O(1)                   |
| Insert beginning   | O(n)              | O(1)                   |
| Memory usage       | Lower             | Higher                 |
| Cache performance  | Better            | Worse                  |
| Best use           | Reading/searching | Frequent insert/remove |

---

# Chapter Summary

In this chapter, you learned:

* `LinkedList` stores elements as connected nodes.
* Each node contains data and references.
* Insertions/removals can be efficient because nodes are only reconnected.
* Accessing elements is slower because traversal is required.
* LinkedList consumes more memory than ArrayList.
* It is useful for queue/deque scenarios and frequent modifications.

The most important idea:

> `LinkedList` optimizes structural changes, while `ArrayList` optimizes access.

---

# ✔️ Next Step

In **Chapter 05 — ArrayList vs LinkedList**, we will perform a complete comparison between both implementations, analyze their performance trade-offs, discuss real-world scenarios, and determine which one should usually be preferred in professional Java development.
