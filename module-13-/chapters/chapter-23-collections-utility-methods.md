# Chapter 23 — Collections Utility Methods

Throughout this module, we learned the main collection structures:

* `List`
* `Set`
* `Queue`
* `Map`

and how to manipulate them manually.

Java also provides a utility class with ready-to-use operations:

```java id="v8j9e1"
java.util.Collections
```

This class contains **static helper methods** for working with collections.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What the `Collections` class is.
* Difference between `Collection` and `Collections`.
* How to manipulate lists using utility methods.
* How to find minimum and maximum values.
* How to count occurrences.
* How to create immutable collections.

---

# Collection vs Collections

This confusion is very common.

---

# Collection

`Collection` is an interface.

It represents:

```text id="1g8d6v"
A group of objects
```

Examples:

```java id="m5k1s8"
List
Set
Queue
```

Hierarchy:

```text id="5f4m8a"
Collection
   |
   +-- List
   +-- Set
   +-- Queue
```

---

# Collections

`Collections` is a utility class.

It provides:

```text id="x6d3q9"
Helper methods
```

Example:

```java id="9j0r2a"
Collections.sort(list);
```

---

# Why Does Collections Exist?

Without utility methods, developers would repeatedly implement:

* Sorting.
* Reversing.
* Shuffling.
* Finding max/min.
* Counting elements.

Java provides tested implementations.

---

# Collections Class Characteristics

All methods are:

```java id="d7m5z1"
static
```

Meaning:

No object creation.

You do:

```java id="g3k9w2"
Collections.method();
```

Not:

```java id="p6m4v8"
new Collections();
```

---

# reverse()

## Purpose

Reverses the order of elements.

---

Example:

```java id="h7x2m9"
List<String> names =
        new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Carlos");
```

Before:

```text id="y8k5q2"
Alice
Bob
Carlos
```

---

Code:

```java id="f3j9n1"
Collections.reverse(names);
```

---

After:

```text id="z9m4p7"
Carlos
Bob
Alice
```

---

# Internal Behavior

`reverse()` swaps elements.

Conceptually:

Before:

```text id="c7w2m6"
[A][B][C][D]
```

After:

```text id="s4q9k1"
[D][C][B][A]
```

---

# Complexity

For a List:

```text id="r6t8m0"
O(n)
```

Every element is visited.

---

# When To Use

Useful for:

* Reverse reports.
* Display latest first.
* Stack-like behavior.

---

# shuffle()

## Purpose

Randomizes the order.

Example:

Before:

```text id="q8f5z3"
1
2
3
4
5
```

Code:

```java id="m4k9v2"
Collections.shuffle(numbers);
```

After:

```text id="w3h7p8"
3
5
1
4
2
```

---

# Internal Behavior

Uses a random swapping algorithm.

Conceptually:

```text id="a9k6y3"
Swap positions randomly
```

---

# Complexity

```text id="v2p7x0"
O(n)
```

---

# Use Cases

* Card games.
* Random questions.
* Randomized lists.

---

# max()

## Purpose

Finds the largest element.

Example:

```java id="r1w5n7"
List<Integer> numbers =
        List.of(10,50,20);
```

Code:

```java id="t9y4m2"
Integer max =
    Collections.max(numbers);
```

Result:

```text id="k7x3p9"
50
```

---

# How Does max() Compare?

It uses:

* Comparable
* Comparator

---

Example:

```java id="f8n2q5"
Collections.max(products);
```

requires Product to have:

```java id="z4m8v1"
Comparable
```

---

Using Comparator:

```java id="x5r9m3"
Collections.max(
    products,
    priceComparator
);
```

---

# Complexity

```text id="b3m7k0"
O(n)
```

Every element must be checked.

---

# min()

## Purpose

Finds the smallest element.

Example:

```java id="e9x6s2"
Integer min =
    Collections.min(numbers);
```

Result:

```text id="n8q4t1"
10
```

---

# Uses Comparable / Comparator

Same as:

```text id="k2v7m5"
max()
```

---

# frequency()

## Purpose

Counts how many times an element appears.

Example:

```java id="g6p3x8"
List<String> names =
    List.of(
        "Java",
        "Python",
        "Java"
    );
```

Code:

```java id="h4m8q0"
int count =
    Collections.frequency(
        names,
        "Java"
    );
```

Result:

```text id="u7w2n6"
2
```

---

# Internal Behavior

Conceptually:

```text id="s8k3p5"
for each element:

    compare

    count matches
```

---

# Complexity

```text id="v9m5z7"
O(n)
```

---

# Use Cases

* Counting words.
* Statistics.
* Validation.

---

# unmodifiableList()

Now we enter an important concept:

## Immutable Collections

Sometimes you want:

> "Create a collection that nobody can modify."

Example:

Configuration data:

```text id="h5n8v3"
Application settings
```

should not change.

---

Create:

```java id="q1x7m9"
List<String> names =
    new ArrayList<>();

names.add("Java");


List<String> immutable =
    Collections.unmodifiableList(names);
```

---

Now:

```java id="p4w8k6"
immutable.add("Python");
```

throws:

```text id="r7m3x1"
UnsupportedOperationException
```

---

# Important Detail

`unmodifiableList()` does not create a copy.

Example:

```java id="n2k9v5"
names.add("Spring");
```

The original list changes.

The wrapper sees the change.

---

Concept:

```text id="d6q1z8"
Original List

      |
      v

Unmodifiable View
```

---

# True Immutable Copy

Modern Java:

```java id="z3m7q9"
List<String> copy =
    List.copyOf(names);
```

This creates an immutable copy.

---

# Collections.unmodifiableSet()

Same concept:

```java id="f8y4m1"
Set<String> set =
    Collections.unmodifiableSet(
        original
    );
```

---

# Collections.unmodifiableMap()

For maps:

```java id="x7q2m8"
Map<Integer,String> map =
    Collections.unmodifiableMap(
        original
    );
```

---

# Sorting Reminder

Collections also provides:

```java id="j4n8v2"
Collections.sort()
```

Example:

```java id="k6m9p3"
Collections.sort(names);
```

We already studied sorting with:

* Comparable.
* Comparator.

---

# reverseOrder()

Creates a reverse comparator.

Example:

```java id="s5w8q1"
Collections.sort(
    numbers,
    Collections.reverseOrder()
);
```

Result:

```text id="p9m2x7"
50
30
10
```

---

# swap()

Swaps two positions.

Example:

```java id="a3k7m9"
Collections.swap(
    list,
    0,
    2
);
```

Before:

```text id="r8q5n2"
A B C
```

After:

```text id="m6v3x8"
C B A
```

---

# fill()

Replaces all elements.

Example:

```java id="w4p9z1"
Collections.fill(
    list,
    "Java"
);
```

Before:

```text id="h7k2m5"
A B C
```

After:

```text id="u9x4q6"
Java Java Java
```

---

# replaceAll()

Replace matching values.

Example:

```java id="y5m8p2"
Collections.replaceAll(
    names,
    "Java",
    "Spring"
);
```

---

# Collection Utilities Summary

| Method             | Purpose              |
| ------------------ | -------------------- |
| sort()             | Sort collection      |
| reverse()          | Reverse order        |
| shuffle()          | Randomize order      |
| max()              | Largest element      |
| min()              | Smallest element     |
| frequency()        | Count occurrences    |
| swap()             | Exchange positions   |
| fill()             | Replace all values   |
| unmodifiableList() | Prevent modification |

---

# Common Mistakes

## Mistake 1 — Confusing Collection and Collections

Remember:

```text id="v4q7m9"
Collection = interface

Collections = utility class
```

---

## Mistake 2 — Expecting unmodifiableList to copy

It creates a view.

---

## Mistake 3 — Using max/min without comparison

Custom objects need:

* Comparable.
* Comparator.

---

## Mistake 4 — Modifying immutable collections

Example:

```java id="k8p3z5"
list.add()
```

will fail.

---

# Practical Example — Library Reports

Imagine our final project:

## Books sorted alphabetically

```java id="w6n2q4"
Collections.sort(books);
```

---

## Display newest first

```java id="z8m4p1"
Collections.reverse(books);
```

---

## Find most expensive book

```java id="q3x7m9"
Collections.max(
    books,
    priceComparator
);
```

---

## Protect configuration

```java id="r5v8k2"
Collections.unmodifiableList(
    books
);
```

---

# Chapter Summary

You learned:

* `Collections` is a helper utility class.
* It provides common collection operations.
* Methods include:

  * reversing,
  * sorting,
  * searching,
  * counting,
  * protecting collections.
* Utility methods reduce duplicated code.

The key idea:

> Collections store data. Collections utilities manipulate that data.

---

# ✔️ Next Step

In **Chapter 24 — Collections Performance and Big-O Comparison**, we will consolidate everything learned so far. We will compare:

* ArrayList vs LinkedList
* HashSet vs TreeSet
* HashMap vs TreeMap
* Queue implementations

and learn how to choose collections based on performance and application requirements.
