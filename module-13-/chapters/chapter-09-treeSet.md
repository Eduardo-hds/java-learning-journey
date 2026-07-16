# Chapter 09 — TreeSet

Until now, we studied two types of `Set`:

* `HashSet` → unique elements, fastest lookup, no order.
* `LinkedHashSet` → unique elements, preserves insertion order.

Now we reach the third major implementation:

```java
TreeSet
```

`TreeSet` solves a different problem:

> "I need unique elements, but I also need them automatically sorted."

Examples:

* Ranking systems.
* Leaderboards.
* Sorted names.
* Price ranges.
* Ordered reports.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `TreeSet` is.
* Why it exists.
* How it maintains sorted elements.
* The concept of tree structures.
* How `Comparable` and `Comparator` interact with `TreeSet`.
* Performance characteristics.
* Memory considerations.
* When to use and avoid `TreeSet`.

---

# What is TreeSet?

`TreeSet` is a `Set` implementation that:

* prevents duplicates,
* keeps elements sorted,
* does not allow index access.

Example:

```java id="vny3kj"
Set<Integer> numbers = new TreeSet<>();

numbers.add(50);
numbers.add(10);
numbers.add(30);
numbers.add(20);
```

Output:

```text id="6v3p9k"
10
20
30
50
```

The order is automatically maintained.

---

# Why Does TreeSet Exist?

Imagine storing employee salaries.

You need:

```text id="n7up0j"
3000
4500
7000
9000
```

A `HashSet`:

```text id="8p4vly"
9000
3000
7000
4500
```

No ordering.

A `LinkedHashSet`:

```text id="k6q5c0"
9000
3000
7000
4500
```

Keeps insertion order, but not sorted.

`TreeSet`:

```text id="k7v7dl"
3000
4500
7000
9000
```

Exactly what we need.

---

# Internal Implementation

`TreeSet` is based on a tree structure.

Conceptually:

```text id="o5ef2b"
              50
             /  \
           30    70
          / \    /
        20 40  60
```

More specifically:

```text id="89y6jb"
Balanced Binary Search Tree
```

Java uses a structure called:

```text id="5q1q34"
Red-Black Tree
```

You do not need to implement one manually, but understanding the idea is important.

---

# Binary Search Tree Concept

A binary search tree follows rules:

For a node:

Left side:

```text
smaller values
```

Right side:

```text
larger values
```

Example:

```text id="8m9w87"
        50

       /  \

     20    80

    / \    / \

  10 30  70 90
```

The tree structure allows searching efficiently.

---

# How TreeSet Adds Elements

Example:

```java id="k7v3fm"
numbers.add(40);
```

Java compares:

Existing values:

```text id="0q4tdd"
50
30
```

Decision:

```text id="4z0q8k"
40 < 50

go left

40 > 30

go right
```

The correct position is found.

---

# Sorting Requirement

A very important rule:

Elements inside a `TreeSet` must know how to compare.

Java needs to answer:

> "Which element comes before another?"

There are two ways:

1. `Comparable`
2. `Comparator`

---

# Comparable

`Comparable` defines the natural ordering of a class.

Example:

```java id="j9k3d5"
class Product implements Comparable<Product>{

}
```

You implement:

```java id="m5yh0q"
compareTo()
```

Example:

```java id="r8m9eq"
@Override
public int compareTo(Product other){

    return this.name.compareTo(other.name);

}
```

Now products know their natural order.

---

# Comparator

Sometimes one natural order is not enough.

Example:

Products can be sorted by:

* name,
* price,
* quantity.

A `Comparator` creates external sorting rules.

Example:

```java id="8v8y3k"
Comparator<Product> priceComparator =
    (p1, p2) ->
    Double.compare(
        p1.getPrice(),
        p2.getPrice()
    );
```

Then:

```java id="2x0m0h"
TreeSet<Product> products =
    new TreeSet<>(priceComparator);
```

Now the tree sorts by price.

---

# Duplicate Detection in TreeSet

This is a very important difference.

`HashSet` uses:

```text id="zjq2hk"
hashCode()
equals()
```

`TreeSet` uses:

```text id="prj3c6"
compareTo()
```

or:

```text id="yl7z9h"
Comparator
```

If comparison returns:

```java id="s7p7fy"
0
```

TreeSet considers them duplicates.

Example:

```java id="u1hx2p"
compareTo() == 0
```

means:

```text id="5byj4y"
"These elements are equivalent"
```

---

# Example Problem

Imagine:

```java
class Student {

    String name;
    int age;

}
```

TreeSet sorted by age:

```text
Alice 20
Bob 25
Carlos 30
```

Two students:

```text
Alice 20
Maria 20
```

If comparison only uses age:

```java
return this.age - other.age;
```

Result:

```text
compareTo() == 0
```

TreeSet thinks they are duplicates.

Maria disappears.

Therefore comparison logic must be carefully designed.

---

# Basic Operations

## Adding

```java id="6n2z2h"
Set<Integer> numbers = new TreeSet<>();

numbers.add(40);
numbers.add(10);
numbers.add(30);
```

Result:

```text id="r8f0dv"
10
30
40
```

---

## Removing

```java id="n1yq5m"
numbers.remove(30);
```

---

## Searching

```java id="dy7y5t"
numbers.contains(40);
```

Tree traversal is used.

---

# Special TreeSet Methods

Because `TreeSet` is sorted, it provides additional operations.

Example:

```java id="f0h6mb"
TreeSet<Integer> numbers = new TreeSet<>();
```

---

## first()

Returns smallest element.

```java id="9a2c9z"
numbers.first();
```

---

## last()

Returns largest element.

```java id="l4l6qw"
numbers.last();
```

---

## higher()

Element greater than a value.

```java id="f1n5m8"
numbers.higher(30);
```

---

## lower()

Element smaller than a value.

```java id="v5v7gy"
numbers.lower(30);
```

---

# Time Complexity

Because it uses a balanced tree:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| contains  | O(log n)   |
| first     | O(log n)   |
| last      | O(log n)   |

---

# Comparing Set Implementations

| Feature         | HashSet | LinkedHashSet   | TreeSet  |
| --------------- | ------- | --------------- | -------- |
| Unique elements | ✅       | ✅               | ✅        |
| Insertion order | ❌       | ✅               | ❌        |
| Sorted order    | ❌       | ❌               | ✅        |
| Average add     | O(1)    | O(1)            | O(log n) |
| Memory          | Lower   | Medium          | Higher   |
| Uses            | Hashing | Hashing + links | Tree     |

---

# Memory Considerations

TreeSet nodes need:

* stored value,
* left reference,
* right reference,
* tree balancing information.

Conceptually:

```text id="7v1z1n"
       Node

+-------------+
| Data        |
| Left        |
| Right       |
| Metadata    |
+-------------+
```

More memory than `HashSet`.

---

# Advantages of TreeSet

## 1. Automatic Sorting

No manual sorting required.

---

## 2. Range Operations

Useful methods:

```java id="yr6v93"
higher()
lower()
subSet()
```

---

## 3. Unique + Ordered Data

Combines both requirements.

---

# Disadvantages of TreeSet

## 1. Slower than HashSet

Because every operation requires tree navigation.

---

## 2. Requires Comparison Logic

Objects must be comparable.

---

## 3. No Random Access

Still no:

```java
get(index)
```

---

# When Should You Use TreeSet?

Use it when:

✅ You need unique elements.

AND:

✅ You need them sorted automatically.

Examples:

* Ranking systems.
* Sorted reports.
* Price ranges.
* Ordered identifiers.

---

# When Should You NOT Use TreeSet?

Avoid it when:

❌ You only need uniqueness.

Use:

```java
HashSet
```

---

❌ You only need insertion order.

Use:

```java
LinkedHashSet
```

---

❌ You need duplicates.

Use:

```java
List
```

---

# Practical Example — Ranking System

Imagine a game leaderboard.

Players:

```text
Carlos - 500 points
Ana - 900 points
Bob - 700 points
```

A TreeSet sorted by points gives:

```text
Ana - 900
Bob - 700
Carlos - 500
```

No extra sorting step required.

---

# Common Mistakes

## Mistake 1 — Expecting insertion order

Wrong:

```java
TreeSet<Integer> numbers = new TreeSet<>();

numbers.add(50);
numbers.add(10);
```

Output:

```text
10
50
```

Not:

```text
50
10
```

---

## Mistake 2 — Bad compareTo implementation

Returning:

```java
0
```

means:

"these objects are duplicates."

Be careful.

---

## Mistake 3 — Using TreeSet when HashSet is enough

You pay the cost of sorting.

---

# Chapter Summary

In this chapter, you learned:

* `TreeSet` stores unique elements in sorted order.
* It uses a balanced tree internally.
* Sorting depends on `Comparable` or `Comparator`.
* Duplicate detection is based on comparison results.
* It is slower than hash-based sets but provides ordering.
* It is ideal when uniqueness and sorting are both required.

The key idea:

> TreeSet trades some performance for automatic ordering.

---

# ✔️ Next Step

In **Chapter 10 — Comparing Set Implementations**, we will consolidate everything learned about `HashSet`, `LinkedHashSet`, and `TreeSet`, create decision rules for choosing between them, and analyze real-world scenarios where each one is the correct solution.
