# Chapter 40 — Collection Utility Methods (Part 1)

Throughout this module, we have worked directly with collection implementations:

```text id="q4m8x2"
ArrayList
HashSet
HashMap
LinkedList
PriorityQueue
```

But Java also provides a helper class:

```java id="x7m3q9"
Collections
```

Important:

Do not confuse:

```text id="m8q2p5"
Collection
```

with:

```text id="v5m9x3"
Collections
```

They are different.

---

# Collection vs Collections

## Collection

Interface.

Represents a group of objects.

Example:

```java id="p3x8m6"
List<String> names;
```

---

Hierarchy:

```text id="r7m2q5"
Collection

 |
 +-- List
 |
 +-- Set
 |
 +-- Queue
```

---

## Collections

Utility class.

Contains:

* Static methods.
* Algorithms.
* Helpers.

Example:

```java id="z5m8x2"
Collections.sort(list);
```

---

# Why Does Collections Exist?

Java collections provide storage.

But common operations are not the responsibility of:

```text id="n6m3x9"
ArrayList
HashSet
```

Example:

Sorting a list:

```java
Collections.sort(list);
```

Instead of:

```text id="c8q4m1"
Every List implementation
creates its own sorting method.
```

---

The utility class centralizes common algorithms.

---

# Collections Utility Methods

Main methods:

```text id="w7m2x8"
reverse()
shuffle()
max()
min()
frequency()
unmodifiableList()
```

---

We will start with:

* `reverse()`
* `shuffle()`

---

# Part 1 — Collections.reverse()

Purpose:

> Reverse the order of elements in a List.

---

Example:

Before:

```text id="x3m8q5"
[
A,
B,
C,
D
]
```

After:

```text id="k7q2m9"
[
D,
C,
B,
A
]
```

---

# Syntax

```java id="m5x9q3"
Collections.reverse(list);
```

---

# Example

Create:

```java id="n8m3q7"
List<String> names =
        new ArrayList<>();


names.add("John");
names.add("Maria");
names.add("Carlos");
```

---

Current:

```text id="h4q8m2"
John
Maria
Carlos
```

---

Apply:

```java id="v6m2x9"
Collections.reverse(names);
```

---

Result:

```text id="p5m8q3"
Carlos
Maria
John
```

---

# Important

`reverse()` modifies the original list.

Before:

```java id="x9m3q5"
names
```

After:

```java id="w7m2x8"
same names object
changed order
```

---

It does NOT create:

```text id="r4q9m1"
new List
```

---

# Complexity

For ArrayList:

```text id="k5m8x2"
O(n)
```

Because every element must be repositioned.

---

# When To Use

Examples:

## Display newest first

Original:

```text id="m8q3x5"
Old
Middle
New
```

Reverse:

```text id="v4m9x2"
New
Middle
Old
```

---

## Undo history

```text id="p7m3q8"
Last action first
```

---

# When NOT To Use

Do not use:

```java id="z3m8x5"
Collections.reverse()
```

when you only need temporary reversed display.

Instead consider creating a copy:

```java id="q6m2x9"
List<String> copy =
        new ArrayList<>(names);
```

Then:

```java
Collections.reverse(copy);
```

---

# Part 2 — Collections.shuffle()

Purpose:

> Randomly rearrange elements.

---

Example:

Before:

```text id="c5m8q2"
[
1,
2,
3,
4
]
```

After:

```text id="j7m3x9"
[
3,
1,
4,
2
]
```

---

# Syntax

```java id="x8m2q5"
Collections.shuffle(list);
```

---

# Example

```java id="f4m9x3"
List<String> cards =
        new ArrayList<>();


cards.add("Ace");
cards.add("King");
cards.add("Queen");
cards.add("Jack");
```

---

Before:

```text id="n5q8m2"
Ace
King
Queen
Jack
```

---

Shuffle:

```java id="v3m7x9"
Collections.shuffle(cards);
```

---

Possible result:

```text id="p8m2x5"
Queen
Ace
Jack
King
```

---

# Internal Idea

Java uses a randomization algorithm to swap positions.

Conceptually:

```text id="r6m3q8"
Choose random position

Swap elements

Repeat
```

---

# Complexity

```text id="w5m9x2"
O(n)
```

Every element participates in the shuffle process.

---

# Real Applications

## Card games

```text id="q7m3x5"
Shuffle deck
```

---

## Quiz systems

```text id="m4x8q2"
Random question order
```

---

## Testing

```text id="z6m2p9"
Randomize test data
```

---

# Part 3 — Collections.reverse() With Objects

Works with custom objects too.

Example:

```java id="k8m3x5"
List<Product> products;
```

---

Before:

```text id="x5q9m2"
Keyboard
Mouse
Monitor
```

---

Reverse:

```java id="v7m3q8"
Collections.reverse(products);
```

---

After:

```text id="p4m8x1"
Monitor
Mouse
Keyboard
```

---

No need for:

* Comparable.
* Comparator.

Because we are only changing positions.

---

# Part 4 — Combining Methods

Example:

```java id="n8q3m5"
Collections.shuffle(products);

Collections.reverse(products);
```

---

Flow:

```text id="h5m9x2"
Original

↓

Random order

↓

Reverse random order
```

---

# Common Mistakes

---

## Mistake 1 — Confusing Collection and Collections

Wrong:

```java id="q7m3x9"
Collection.sort()
```

Correct:

```java id="x4m8p2"
Collections.sort()
```

---

## Mistake 2 — Expecting reverse() to return a list

Wrong:

```java id="m8q3x5"
List<String> reversed =
        Collections.reverse(names);
```

Why?

Because:

```java id="z5m2x8"
reverse()
```

returns:

```text id="v7m9q3"
void
```

---

Correct:

```java id="c4x8m2"
Collections.reverse(names);
```

---

## Mistake 3 — Using shuffle when order matters

Do not shuffle:

* Financial reports.
* Sorted rankings.
* User data.

---

# Practical Example — Library System

Our final project:

```text id="r8m3q5"
Library Management System
```

May use:

---

Display books alphabetically:

```text id="w5q2m8"
TreeSet
```

---

Random recommendation:

```java id="x7m3q9"
Collections.shuffle()
```

---

Reverse borrowing history:

```java id="p4m8x2"
Collections.reverse()
```

---

# Exercise Task

Create:

```java id="m6q3x8"
List<String> books
```

Add:

```text id="v8m2q5"
Java
Clean Code
Algorithms
Design Patterns
```

Practice:

1. Reverse the list.
2. Shuffle the list.
3. Print after each operation.

Observe that the original list changes.

---

# ✔️ Next Step

In **Chapter 41 — Collection Utility Methods (Part 2)** we will complete the `Collections` class:

* `max()`
* `min()`
* `frequency()`
* `unmodifiableList()`

Then we will move toward the final project:

**Library Management System**.
