# Chapter 24 — Collections Performance and Big-O Comparison

Throughout this module, we learned many collection types:

* `ArrayList`
* `LinkedList`
* `HashSet`
* `TreeSet`
* `HashMap`
* `LinkedHashMap`
* `TreeMap`
* `Queue`
* `Deque`

Now we need to answer the most important professional question:

> "Which collection should I choose for this problem?"

The answer depends on:

* How data is accessed.
* How often data changes.
* Whether ordering matters.
* Whether sorting is necessary.
* Memory requirements.

---

# Learning Objectives

By the end of this chapter, you should understand:

* Big-O notation in collections.
* Operation costs.
* Performance trade-offs.
* When to prioritize speed.
* When to prioritize ordering.
* When to prioritize memory.

---

# Big-O Introduction

Big-O describes how the cost of an operation grows as data increases.

Example:

Imagine searching a list.

With:

```text id="r9x4m1"
10 items
```

A slow operation may be acceptable.

But with:

```text id="g8k2p6"
10 million items
```

the difference becomes enormous.

---

# Common Complexities

## O(1) — Constant Time

The operation takes the same time regardless of size.

Example:

```java id="h3m7q8"
map.get(key);
```

With:

```text id="m5x1z7"
10 entries
```

or:

```text id="p9v4k2"
10 million entries
```

the average access remains constant.

---

## O(log n) — Logarithmic

The structure reduces the search space.

Example:

Tree search.

Every step eliminates half the possibilities.

---

## O(n) — Linear

The operation checks every element.

Example:

Searching a list:

```java id="q7m2v9"
list.contains(value);
```

---

## O(n²) — Quadratic

Usually nested loops.

Example:

Comparing every item with every other item.

---

# ArrayList Performance

Internal structure:

```text id="z6k8p1"
Dynamic Array
```

Example:

```text id="m4x9q2"
[0][1][2][3]
```

---

# ArrayList Operations

| Operation        | Complexity   |
| ---------------- | ------------ |
| get(index)       | O(1)         |
| add(end)         | O(1) average |
| add(position)    | O(n)         |
| remove(end)      | O(1)         |
| remove(position) | O(n)         |
| search           | O(n)         |

---

# Why is get() Fast?

Because indexes directly access memory.

Example:

```java id="v8q2m5"
list.get(100);
```

Java jumps directly.

---

# Why is insertion in the middle slow?

Example:

Before:

```text id="x4m7k9"
[A][B][C][D]
```

Insert X at index 1:

```text id="q8p3v6"
[A][X][B][C][D]
```

Elements must move.

---

# LinkedList Performance

Internal structure:

```text id="n5k9w3"
Doubly Linked List
```

Conceptually:

```text id="p2x8m4"
A ↔ B ↔ C ↔ D
```

---

# LinkedList Operations

| Operation         | Complexity |
| ----------------- | ---------- |
| get(index)        | O(n)       |
| add(beginning)    | O(1)       |
| add(end)          | O(1)       |
| add(middle)       | O(1)*      |
| remove(beginning) | O(1)       |
| remove(end)       | O(1)       |
| search            | O(n)       |

* After reaching the position.

---

# Why is get() Slow?

To reach index 100:

```text id="h6q2m8"
Start

A
B
C
...

100 steps
```

---

# ArrayList vs LinkedList

| Feature           | ArrayList | LinkedList |
| ----------------- | --------- | ---------- |
| Structure         | Array     | Nodes      |
| Random access     | Excellent | Poor       |
| Insert beginning  | Slow      | Fast       |
| Insert end        | Fast      | Fast       |
| Memory            | Lower     | Higher     |
| Cache performance | Better    | Worse      |

---

# Practical Decision

Use:

```java id="d5m8x1"
ArrayList
```

90% of the time.

---

Use:

```java id="k7p3q9"
LinkedList
```

when:

* Frequent insertions/removals at ends.
* Queue/deque behavior.

---

# HashSet Performance

Internal structure:

```text id="w8m2v5"
Hash Table
```

---

Operations:

| Operation | Complexity   |
| --------- | ------------ |
| add       | O(1) average |
| remove    | O(1) average |
| contains  | O(1) average |

---

# Why Is HashSet Fast?

It uses:

```text id="q4n9x7"
hashCode()
```

to find location quickly.

---

# HashSet Limitations

No ordering.

Example:

Insert:

```text id="j5m8q3"
A
B
C
```

Order is not guaranteed.

---

# TreeSet Performance

Internal structure:

```text id="f8x3k6"
Red-Black Tree
```

---

Operations:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| contains  | O(log n)   |

---

# HashSet vs TreeSet

| Feature    | HashSet    | TreeSet   |
| ---------- | ---------- | --------- |
| Speed      | Faster     | Slower    |
| Ordering   | No         | Sorted    |
| Structure  | Hash table | Tree      |
| Comparison | hashCode   | compareTo |

---

# Choosing Set

Need only uniqueness?

```java id="x3q8m1"
HashSet
```

Need sorted uniqueness?

```java id="m9v5p2"
TreeSet
```

---

# HashMap Performance

Internal structure:

```text id="u7k2x9"
Hash Table
```

---

Operations:

| Operation   | Complexity   |
| ----------- | ------------ |
| put         | O(1) average |
| get         | O(1) average |
| remove      | O(1) average |
| containsKey | O(1) average |

---

# LinkedHashMap Performance

Very similar:

| Operation | Complexity |
| --------- | ---------- |
| put       | O(1)       |
| get       | O(1)       |
| remove    | O(1)       |

Difference:

Additional linked list overhead.

---

# TreeMap Performance

Internal structure:

```text id="q5x8m3"
Red-Black Tree
```

---

Operations:

| Operation | Complexity |
| --------- | ---------- |
| put       | O(log n)   |
| get       | O(log n)   |
| remove    | O(log n)   |

---

# Map Comparison

| Feature   | HashMap | LinkedHashMap | TreeMap |
| --------- | ------- | ------------- | ------- |
| Speed     | Highest | High          | Lower   |
| Order     | None    | Insertion     | Sorted  |
| Structure | Hash    | Hash + List   | Tree    |
| Memory    | Lowest  | Medium        | Highest |

---

# Queue Performance

## ArrayDeque

Internal:

```text id="p4m8q2"
Resizable Array
```

Operations:

| Operation   | Complexity |
| ----------- | ---------- |
| addFirst    | O(1)       |
| addLast     | O(1)       |
| removeFirst | O(1)       |
| removeLast  | O(1)       |

---

## PriorityQueue

Internal:

```text id="z6q3m8"
Heap
```

Operations:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| peek      | O(1)       |

---

# Collection Selection Guide

## Need ordered list?

```text id="r8m1x4"
ArrayList
```

---

## Need many insertions/removals at ends?

```text id="v7k5p2"
LinkedList
or
ArrayDeque
```

---

## Need unique elements?

```text id="n3x9m6"
HashSet
```

---

## Need unique + sorted?

```text id="m4q8z2"
TreeSet
```

---

## Need key/value lookup?

```text id="q6x1p8"
HashMap
```

---

## Need key/value + insertion order?

```text id="k9m3v5"
LinkedHashMap
```

---

## Need key/value + sorted keys?

```text id="s2q7x9"
TreeMap
```

---

# Memory Considerations

Performance is not everything.

Example:

## ArrayList

Stores:

```text id="a8m4q2"
References only
```

Low overhead.

---

## LinkedList

Each node stores:

```text id="w5x9p3"
Value
Previous reference
Next reference
```

More memory.

---

## Tree structures

Each node stores:

```text id="e7m2k8"
Value
Children
Parent
Color
```

More overhead.

---

# Common Mistakes

## Mistake 1 — Choosing the fastest collection always

Example:

Using HashMap when sorted data is required.

---

## Mistake 2 — Ignoring data size

A solution working with:

```text id="h4q8m6"
100 items
```

may fail with:

```text id="z7m3p1"
10 million items
```

---

## Mistake 3 — Assuming LinkedList is faster

Many beginners believe:

"LinkedList = faster insertion."

Reality:

Finding the position is expensive.

---

# Professional Rule of Thumb

Most applications:

```text id="k5x9m2"
ArrayList
HashMap
HashSet
```

cover most cases.

Specialized collections are used when requirements demand them.

---

# Chapter Summary

You learned:

* Big-O explains collection performance.
* ArrayList excels at access.
* LinkedList excels at certain insertions/removals.
* Hash collections prioritize speed.
* Tree collections prioritize ordering.
* Choosing collections is a design decision.

The key idea:

> The best collection is not the fastest one. It is the one whose behavior matches the problem.

---

# ✔️ Next Step

In **Chapter 25 — Exercise 1: Student Management System**, we begin the practical exercises of this module.

We will build the first application step-by-step:

* Create the project structure.
* Create the `Student` model.
* Use `ArrayList`.
* Implement:

  * Add student.
  * Remove student.
  * Update student.
  * Search student.

No complete solution will be provided upfront. We will build it incrementally.
