# Chapter 17 — LinkedHashMap

In the previous chapter, we studied `HashMap`, which provides extremely fast access using keys.

However, we saw an important limitation:

```text
HashMap does not guarantee order.
```

Sometimes applications need both:

* Fast lookup by key.
* Predictable iteration order.

Example:

* Displaying a report in the order data was inserted.
* Maintaining user activity history.
* Building simple caches.
* Preserving configuration order.

For this situation, Java provides:

```java
LinkedHashMap
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `LinkedHashMap` is.
* Why it exists.
* How it differs from `HashMap`.
* Internal implementation.
* Insertion order vs access order.
* Performance differences.
* When to use LinkedHashMap.

---

# What is LinkedHashMap?

`LinkedHashMap` is a `Map` implementation that combines:

```text
HashMap
+
Linked List
```

It provides:

1. Fast lookup using hashing.
2. Predictable iteration order.

---

# Simple Example

Using `HashMap`:

```java
Map<Integer, String> map =
        new HashMap<>();

map.put(3, "Carlos");
map.put(1, "Alice");
map.put(2, "Bob");
```

Iteration order:

```text
Could be:

1 → Alice
3 → Carlos
2 → Bob
```

No guarantee.

---

Using `LinkedHashMap`:

```java
Map<Integer, String> map =
        new LinkedHashMap<>();

map.put(3, "Carlos");
map.put(1, "Alice");
map.put(2, "Bob");
```

Iteration:

```text
3 → Carlos
1 → Alice
2 → Bob
```

Insertion order is preserved.

---

# Why Does LinkedHashMap Exist?

A common problem:

You want:

```text
Fast search
+
Remember order
```

A normal HashMap:

```text
Fast
❌ No order
```

A TreeMap:

```text
Sorted
❌ Slower
```

LinkedHashMap:

```text
Fast
+
Insertion order
```

---

# Internal Structure

`LinkedHashMap` extends the idea of `HashMap`.

Conceptually:

```text
Hash Table

Bucket 0

Bucket 1
   |
   Entry

Bucket 2
   |
   Entry
```

But every entry also has links:

```text
Previous
   |
Entry
   |
Next
```

---

# Visualization

Imagine:

Hash table:

```text
Bucket 1 → Alice
Bucket 5 → Carlos
Bucket 8 → Bob
```

Linked list:

```text
Alice ↔ Carlos ↔ Bob
```

The hash table provides:

```text
fast lookup
```

The linked list provides:

```text
order
```

---

# How Insertion Works

Example:

```java
map.put("A", 10);
map.put("B", 20);
map.put("C", 30);
```

Internally:

Hash structure:

```text
A
B
C
```

Linked order:

```text
A → B → C
```

Iteration follows:

```text
A
B
C
```

---

# LinkedHashMap vs HashMap

This is one of the most important comparisons.

---

## HashMap

Structure:

```text
Hash table
```

Advantages:

* Maximum speed.
* Less memory.

Disadvantage:

* No order guarantee.

---

## LinkedHashMap

Structure:

```text
Hash table
+
Linked list
```

Advantages:

* Maintains order.

Disadvantages:

* More memory.
* Slightly slower.

---

# Comparison Table

| Feature    | HashMap       | LinkedHashMap            |
| ---------- | ------------- | ------------------------ |
| Key lookup | O(1) avg      | O(1) avg                 |
| Ordering   | None          | Insertion order          |
| Memory     | Lower         | Higher                   |
| Iteration  | Unpredictable | Predictable              |
| Internal   | Hash table    | Hash table + linked list |

---

# Basic Operations

The API is almost identical to HashMap.

---

# Creating

```java
Map<Integer, String> users =
        new LinkedHashMap<>();
```

---

# Adding

```java
users.put(1, "Alice");
users.put(2, "Bob");
users.put(3, "Carlos");
```

---

# Getting

```java
users.get(2);
```

Result:

```text
Bob
```

---

# Removing

```java
users.remove(1);
```

---

# Iterating

```java
for(Map.Entry<Integer,String> entry :
        users.entrySet()){

    System.out.println(
        entry.getKey()
    );

    System.out.println(
        entry.getValue()
    );
}
```

Output:

```text
1 → Alice
2 → Bob
3 → Carlos
```

---

# Access Order

One interesting feature:

`LinkedHashMap` can also maintain:

```text
access order
```

instead of:

```text
insertion order
```

---

# Insertion Order

Default behavior:

```java
new LinkedHashMap<>();
```

Order:

```text
Inserted order
```

Example:

Insert:

```text
A
B
C
```

Iteration:

```text
A
B
C
```

---

# Access Order

You can create:

```java
LinkedHashMap<K,V> map =
    new LinkedHashMap<>(16,0.75f,true);
```

The last parameter:

```java
true
```

means:

```text
accessOrder
```

---

# Example

Insert:

```text
A
B
C
```

Current order:

```text
A
B
C
```

Access:

```java
map.get(A);
```

Order becomes:

```text
B
C
A
```

Because A was recently used.

---

# Why Access Order Matters?

This behavior is useful for:

```text
LRU Cache
```

Meaning:

```text
Least Recently Used
```

Example:

Cache capacity:

```text
3 items
```

Stored:

```text
A B C
```

Access:

```text
A
```

Now:

```text
B C A
```

Insert:

```text
D
```

Remove:

```text
B
```

because it was least recently used.

---

# Time Complexity

Average:

| Operation   | Complexity |
| ----------- | ---------- |
| put         | O(1)       |
| get         | O(1)       |
| remove      | O(1)       |
| containsKey | O(1)       |

Similar to HashMap.

---

# Why Slightly Slower Than HashMap?

Because every entry maintains:

```text
Previous reference
Next reference
```

Extra work:

* Updating links.
* Maintaining order.

---

# Memory Considerations

HashMap entry:

```text
Key
Value
Hash
```

LinkedHashMap entry:

```text
Key
Value
Hash
Previous
Next
```

More references mean:

```text
More memory usage
```

---

# Advantages of LinkedHashMap

## 1. Predictable Iteration

Useful for:

* Reports.
* Logs.
* Ordered displays.

---

## 2. Fast Lookup

Maintains HashMap performance.

---

## 3. Supports LRU Cache Patterns

Using access order.

---

# Disadvantages of LinkedHashMap

## 1. More Memory

Compared with HashMap.

---

## 2. Slightly Slower

Extra linked list management.

---

## 3. No Sorting

It preserves insertion order, not sorted order.

---

# LinkedHashMap vs TreeMap

Another important comparison.

---

## LinkedHashMap

Order:

```text
Insertion
```

Example:

Insert:

```text
50
10
30
```

Result:

```text
50
10
30
```

---

## TreeMap

Order:

```text
Sorted keys
```

Result:

```text
10
30
50
```

---

# Comparison

| Feature   | LinkedHashMap    | TreeMap     |
| --------- | ---------------- | ----------- |
| Structure | Hash + List      | Tree        |
| Order     | Insertion        | Sorted      |
| Lookup    | O(1) avg         | O(log n)    |
| Memory    | Higher           | Higher      |
| Use       | Preserve history | Sorted data |

---

# When Should You Use LinkedHashMap?

Use when:

## Need fast lookup + order

Examples:

* Ordered reports.
* User history.
* Configuration loading.
* Cache implementations.

---

# When Should You NOT Use LinkedHashMap?

Avoid when:

## Order does not matter

Use:

```java
HashMap
```

---

## Keys must be sorted

Use:

```java
TreeMap
```

---

## You only need values

Use:

```java
List
```

or:

```java
Set
```

---

# Practical Example — User Activity History

Imagine:

```text
User actions:

LOGIN
SEARCH
PURCHASE
```

Using:

```java
Map<Integer,String> history =
        new LinkedHashMap<>();
```

Store:

```text
1 → LOGIN
2 → SEARCH
3 → PURCHASE
```

When displaying:

```text
LOGIN
SEARCH
PURCHASE
```

The order is preserved.

---

# Common Mistakes

## Mistake 1 — Thinking LinkedHashMap sorts

It does not.

It preserves insertion order.

---

## Mistake 2 — Choosing LinkedHashMap automatically

If order is irrelevant:

```java
HashMap
```

is usually better.

---

## Mistake 3 — Confusing access order and insertion order

Default:

```text
Insertion order
```

Special configuration:

```text
Access order
```

---

# Chapter Summary

You learned:

* `LinkedHashMap` combines hashing and linked ordering.
* It maintains predictable iteration order.
* It has similar performance to HashMap.
* It uses extra memory to maintain links.
* It can maintain insertion order or access order.
* It is useful for ordered data and cache-like structures.

The key idea:

> LinkedHashMap is HashMap when you need to remember the path elements arrived.

---

# ✔️ Next Step

In **Chapter 18 — TreeMap**, we will study the Map implementation that keeps keys sorted. You will learn how trees organize data, why operations become O(log n), and when sorted maps are preferable over hash-based maps.
