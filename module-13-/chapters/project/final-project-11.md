# Chapter 55 — Module Review: Collections Framework Deep Review (Part 1)

We have finished the implementation of the **Library Management System**.

Now we will consolidate the knowledge from this module.

The objective of this review is not memorization.

The goal is to develop the ability to answer:

> "Given a problem, which collection should I choose and why?"

---

# Collections Framework Overview

The Java Collections Framework is a group of:

* Interfaces.
* Implementations.
* Algorithms.
* Utility methods.

Designed to store and manipulate groups of objects.

---

# Before Collections: Arrays

Before collections, Java developers commonly used arrays.

Example:

```java
int[] numbers = new int[10];
```

---

Arrays have limitations:

## Fixed Size

Created with:

```java
new int[10]
```

The size cannot change.

---

Example:

Need 20 elements?

Create another array.

---

## No Built-in Operations

Searching:

```java
for(int number : numbers)
```

Sorting:

Need:

```java
Arrays.sort()
```

---

## Only Index Access

Example:

```java
numbers[5]
```

You access by position.

---

# Collections Improve This

Example:

```java
List<Integer> numbers =
        new ArrayList<>();
```

---

Advantages:

* Dynamic size.
* Built-in operations.
* Different behaviors.
* Better abstraction.

---

# Collections Hierarchy

The main hierarchy:

```text id="1o5h8s"

              Iterable

                  |

              Collection

                  |

       +----------+----------+

       |          |          |

      List       Set       Queue


```

---

Important:

`Map` is separate.

```text id="m7q3x9"

              Map

               |

     +---------+---------+

     |         |         |

 HashMap  TreeMap  LinkedHashMap

```

---

# Iterable Interface

The root of iteration.

Interface:

```java
Iterable<T>
```

---

Provides:

```java
iterator()
```

---

Example:

```java
for(Book book : books){

}
```

---

Behind the scenes:

Java uses:

```java
Iterator
```

---

# Collection Interface

Represents groups of objects.

Methods:

Examples:

```java
add()

remove()

contains()

size()

isEmpty()
```

---

Implemented by:

```text
List

Set

Queue
```

---

# List Review

A List represents:

> An ordered collection that allows duplicates.

---

Characteristics:

* Maintains insertion order.
* Allows repeated elements.
* Uses indexes.

---

Example:

```text
Position:

0 → Book A

1 → Book B

2 → Book A
```

---

Main implementations:

* ArrayList.
* LinkedList.

---

# ArrayList

Internal structure:

```text
Dynamic Array
```

Conceptually:

```text
[index]

0  Book A
1  Book B
2  Book C
```

---

When capacity is full:

Java creates:

```text
larger array

copies elements

continues
```

---

# ArrayList Performance

| Operation       | Complexity   |
| --------------- | ------------ |
| Access by index | O(1)         |
| Add end         | O(1) average |
| Search          | O(n)         |
| Remove middle   | O(n)         |

---

# Why Access Is Fast?

Because:

```java
list.get(10);
```

directly calculates:

```text
memory position
```

---

# Why Remove Is Slow?

Example:

Before:

```text
A B C D E
```

Remove:

```text
C
```

Need:

```text
A B D E
```

Elements shift.

---

# When To Use ArrayList

Use when:

✅ Mostly reading data.

✅ Access by position.

✅ Add elements at end.

Example:

```text
Product list

Books catalog

Search results
```

---

# When NOT To Use ArrayList

Avoid when:

❌ Constant insertion/removal at beginning.

Example:

```text
Queue simulation
```

---

# LinkedList

Internal structure:

Nodes connected together.

Conceptually:

```text
Node

[value]

  |

next

  |

Node

[value]

  |

next
```

---

Each element stores:

* Value.
* Reference to next node.

---

# LinkedList Performance

| Operation        | Complexity |
| ---------------- | ---------- |
| Add beginning    | O(1)       |
| Remove beginning | O(1)       |
| Search           | O(n)       |
| Access index     | O(n)       |

---

# Why get(index) Is Slow?

Example:

```java
list.get(500);
```

LinkedList must:

```text
start at first node

follow links

reach position 500
```

---

# ArrayList vs LinkedList

| Feature            | ArrayList | LinkedList |
| ------------------ | --------- | ---------- |
| Internal structure | Array     | Nodes      |
| Random access      | Excellent | Poor       |
| Memory usage       | Lower     | Higher     |
| Add end            | Fast      | Fast       |
| Insert beginning   | Slow      | Fast       |
| Search             | Same      | Same       |

---

# Practical Decision

Most applications:

```java
ArrayList
```

is the default choice.

---

LinkedList is useful when:

* Frequent insertion/removal at ends.
* Need deque behavior.

---

# Set Review

A Set represents:

> A collection that does not allow duplicates.

---

Characteristics:

* No repeated elements.
* No index.
* Depends on implementation for ordering.

---

Implementations:

* HashSet.
* LinkedHashSet.
* TreeSet.

---

# HashSet

Internal structure:

```text
Hash Table
```

---

Uses:

```text
hashCode()

equals()
```

---

Adding:

```java
set.add(object);
```

Process:

```text
hashCode()

↓

bucket

↓

equals()
```

---

# HashSet Performance

| Operation | Complexity   |
| --------- | ------------ |
| add       | O(1) average |
| remove    | O(1) average |
| contains  | O(1) average |

---

# When To Use HashSet

Use when:

✅ Need uniqueness.

✅ Do not care about order.

Examples:

```text
Unique categories

Unique permissions

Unique tags
```

---

# LinkedHashSet

Same as HashSet but maintains:

```text
Insertion order
```

Example:

Input:

```text
Java

Python

C++
```

Output:

```text
Java

Python

C++
```

---

Performance:

Slightly more memory.

---

# TreeSet

Internal structure:

```text
Tree structure
```

Usually:

Red-Black Tree.

---

Maintains:

```text
Sorted order
```

---

Example:

Input:

```text
Java

Algorithms

Clean Code
```

Output:

```text
Algorithms

Clean Code

Java
```

---

Performance:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| search    | O(log n)   |

---

# HashSet vs LinkedHashSet vs TreeSet

| Feature   | HashSet    | LinkedHashSet   | TreeSet |
| --------- | ---------- | --------------- | ------- |
| Duplicate | No         | No              | No      |
| Order     | None       | Insertion       | Sorted  |
| Speed     | Fastest    | Slightly slower | Slowest |
| Structure | Hash table | Hash + links    | Tree    |

---

# Exercise Task

Answer without looking:

---

## 1

You need:

```text
Fast search by ID
```

Which collection?

---

## 2

You need:

```text
Keep elements sorted automatically
```

Which collection?

---

## 3

You need:

```text
Allow duplicates and maintain order
```

Which collection?

---

## 4

You need:

```text
Unique values, no order needed
```

Which collection?

---

# ✔️ Next Step

In **Chapter 56 — Module Review: Map, Queue, Iterators and Performance Comparison** we will finish the review with:

* HashMap internals.
* TreeMap vs LinkedHashMap.
* Queue and Deque.
* Iterator and ListIterator.
* Complete collection decision guide.
