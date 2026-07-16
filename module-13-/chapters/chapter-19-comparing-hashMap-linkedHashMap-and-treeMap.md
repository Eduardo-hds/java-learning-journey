# Chapter 19 — Comparing HashMap, LinkedHashMap, and TreeMap

We have now studied the three main `Map` implementations in Java:

* `HashMap`
* `LinkedHashMap`
* `TreeMap`

All three store:

```text
Key → Value
```

However, they solve different problems.

The important skill is not memorizing classes.

The important skill is answering:

> "What behavior does my application need from this Map?"

---

# Learning Objectives

By the end of this chapter, you should understand:

* The differences between the main Map implementations.
* Internal structure comparison.
* Performance differences.
* Ordering behavior.
* Memory trade-offs.
* How to choose the correct Map.

---

# The Three Questions

Before choosing a Map, ask:

---

## Question 1

Do I need sorting?

If yes:

```java
TreeMap
```

---

## Question 2

Do I need insertion order?

If yes:

```java
LinkedHashMap
```

---

## Question 3

Do I only need fast lookup?

If yes:

```java
HashMap
```

---

# HashMap

## Main Idea

> Fast access using keys.

Example:

```text
User ID → User
```

---

## Internal Structure

Uses:

```text
Hash Table
```

Conceptually:

```text
Bucket 0

Bucket 1
   |
 Key → Value

Bucket 2
```

---

## Ordering

No guarantee.

Example:

Inserted:

```text
3 → Carlos
1 → Alice
2 → Bob
```

Iteration:

Could be:

```text
2 → Bob
3 → Carlos
1 → Alice
```

---

## Performance

Average:

| Operation | Complexity |
| --------- | ---------- |
| put       | O(1)       |
| get       | O(1)       |
| remove    | O(1)       |

---

## Advantages

✅ Fastest lookup.

✅ Lower memory usage.

✅ Most common Map.

---

## Disadvantages

❌ No ordering.

❌ No sorted operations.

---

## Best Use Cases

* Database cache.
* User lookup.
* Product lookup.
* Configuration storage.

---

# LinkedHashMap

## Main Idea

> HashMap + remembering order.

---

## Internal Structure

Uses:

```text
Hash table
+
Doubly linked list
```

Conceptually:

Hash:

```text
Bucket 1 → Alice
Bucket 5 → Carlos
```

Order:

```text
Alice ↔ Carlos ↔ Bob
```

---

## Ordering

Maintains:

```text
Insertion order
```

Default.

Example:

Insert:

```text
B
A
C
```

Iteration:

```text
B
A
C
```

---

## Performance

Average:

| Operation | Complexity |
| --------- | ---------- |
| put       | O(1)       |
| get       | O(1)       |
| remove    | O(1)       |

Very close to HashMap.

---

## Advantages

✅ Fast lookup.

✅ Predictable iteration.

✅ Useful for ordered displays.

---

## Disadvantages

❌ More memory.

❌ Slightly slower.

---

## Best Use Cases

* Reports.
* User history.
* Ordered configurations.
* LRU cache.

---

# TreeMap

## Main Idea

> Keep keys sorted automatically.

---

## Internal Structure

Uses:

```text
Red-Black Tree
```

Conceptually:

```text
          50

       /      \

     20        80

    /
  10
```

---

## Ordering

Keys are sorted.

Example:

Insert:

```text
50
10
30
```

Result:

```text
10
30
50
```

---

## Performance

| Operation | Complexity |
| --------- | ---------- |
| put       | O(log n)   |
| get       | O(log n)   |
| remove    | O(log n)   |

---

## Advantages

✅ Sorted keys.

✅ Range operations.

Example:

```text
Find values between 100 and 500
```

---

## Disadvantages

❌ Slower than HashMap.

❌ More memory.

---

## Best Use Cases

* Rankings.
* Sorted reports.
* Date-based data.
* Range queries.

---

# Complete Comparison

| Feature             | HashMap    | LinkedHashMap      | TreeMap        |
| ------------------- | ---------- | ------------------ | -------------- |
| Ordering            | None       | Insertion          | Sorted         |
| Structure           | Hash table | Hash + Linked List | Red-Black Tree |
| get()               | O(1) avg   | O(1) avg           | O(log n)       |
| put()               | O(1) avg   | O(1) avg           | O(log n)       |
| Memory              | Lower      | Medium             | Higher         |
| Requires comparison | No         | No                 | Yes            |
| Allows null key     | Yes        | Yes                | Limited        |
| Best feature        | Speed      | Order              | Sorting        |

---

# Choosing by Requirement

Let's solve real problems.

---

# Scenario 1 — User Authentication

Requirement:

Find user by username.

Example:

```text
username → User
```

Need:

* Fast lookup.
* No ordering.

Choice:

```java
HashMap<String,User>
```

---

# Scenario 2 — Display Purchase History

Requirement:

Show purchases in the order they happened.

Example:

```text
Purchase 1
Purchase 2
Purchase 3
```

Need:

* Lookup.
* Insertion order.

Choice:

```java
LinkedHashMap
```

---

# Scenario 3 — Ranking System

Requirement:

Display players ordered by score.

Example:

```text
1000 → Player A
800 → Player B
500 → Player C
```

Need:

* Sorted keys.

Choice:

```java
TreeMap
```

---

# Scenario 4 — Cache

Requirement:

Keep recently accessed items.

Need:

* Fast lookup.
* Access order.

Choice:

```java
LinkedHashMap
```

with:

```java
accessOrder=true
```

---

# Scenario 5 — Product Search

Requirement:

Find product by ID.

Example:

```text
12345 → Laptop
```

Need:

* Fast access.

Choice:

```java
HashMap
```

---

# Map Decision Tree

```text
Need a Map?
      |
      |
Need sorted keys?
      |
    Yes
      |
   TreeMap


No
 |
Need insertion/access order?
 |
Yes
 |
LinkedHashMap


No
 |
HashMap
```

---

# Common Mistakes

## Mistake 1 — Always using HashMap

Many developers use HashMap everywhere.

Problem:

Sometimes order matters.

Example:

Displaying menu options.

---

## Mistake 2 — Using TreeMap because "sorted is better"

Sorting has a cost.

If you do not need sorting:

Use:

```java
HashMap
```

---

## Mistake 3 — Confusing insertion order and sorted order

Example:

LinkedHashMap:

```text
Inserted:
50
10
30

Result:
50
10
30
```

TreeMap:

```text
Result:
10
30
50
```

---

## Mistake 4 — Forgetting object comparison

TreeMap with custom objects requires:

* Comparable
* Comparator

---

# Practical Design Example

Imagine a library system.

You need:

## Search books by ISBN

```text
ISBN → Book
```

Use:

```java
HashMap
```

---

## Display recently added books

Use:

```java
LinkedHashMap
```

---

## Generate alphabetical reports

Use:

```java
TreeMap
```

---

One application can use all three.

The correct collection depends on the problem.

---

# Chapter Summary

You learned:

* `HashMap` focuses on speed.
* `LinkedHashMap` focuses on speed + order.
* `TreeMap` focuses on sorted organization.
* The choice depends on behavior requirements.

The key principle:

> Choose a collection based on the operation you need, not because one collection is universally better.

---

# ✔️ Next Step

In **Chapter 20 — Iterators**, we will study how Java traverses collections internally. You will learn why `Iterator` exists, how to safely remove elements while iterating, and why modifying collections during loops can cause problems.
