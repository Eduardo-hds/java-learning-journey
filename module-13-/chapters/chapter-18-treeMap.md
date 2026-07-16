# Chapter 18 — TreeMap

Until now, we studied two important `Map` implementations:

* `HashMap` → fastest lookup, no order.
* `LinkedHashMap` → fast lookup, preserves insertion order.

Now we study:

```java id="l0z7r8"
TreeMap
```

A `TreeMap` solves a different problem:

> "I need my keys to always remain sorted."

Examples:

* Ranking systems.
* Sorted reports.
* Dictionary-like structures.
* Scheduling by date.
* Range searches.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `TreeMap` is.
* Why it exists.
* How it differs from HashMap and LinkedHashMap.
* Internal tree structure.
* Natural ordering.
* Comparator usage.
* Performance characteristics.
* When to use TreeMap.

---

# What is TreeMap?

`TreeMap` is a `Map` implementation where:

```text id="4t2n8z"
Keys are sorted automatically.
```

Example:

```java id="q9pl9m"
Map<Integer, String> users =
        new TreeMap<>();

users.put(50, "Carlos");
users.put(10, "Alice");
users.put(30, "Bob");
```

Iteration:

```text id="75a5yd"
10 → Alice
30 → Bob
50 → Carlos
```

The keys are automatically ordered.

---

# Why Does TreeMap Exist?

Imagine a ranking system:

```text id="d3w8c2"
Score → Player
```

You insert:

```text id="1by0y5"
500 → John
1000 → Maria
700 → Carlos
```

You want:

```text id="i9z0xa"
1000 → Maria
700 → Carlos
500 → John
```

A HashMap cannot provide this.

A TreeMap can.

---

# TreeMap Internal Structure

TreeMap uses:

```text id="7d2g6b"
Red-Black Tree
```

A type of:

```text id="g8o5c1"
Self-balancing binary search tree
```

---

# Binary Search Tree Concept

A tree organizes values using comparison.

Example:

```text id="d93b0s"
             50

          /      \

        20        80

       /  \       /

     10   30    70
```

Rule:

Left side:

```text id="j4pxkj"
Smaller values
```

Right side:

```text id="u1hxcz"
Larger values
```

---

# Why Balance Matters

A normal binary tree can become bad.

Example:

Insert:

```text id="9n4m3p"
10
20
30
40
```

Could become:

```text id="2j2m8s"
10
 \
 20
  \
  30
   \
    40
```

This behaves like a linked list.

Search becomes:

```text id="bqkz4f"
O(n)
```

---

A Red-Black Tree automatically balances itself.

Result:

```text id="8e8q5m"
        20

      /    \

    10      30

              \
               40
```

Operations remain:

```text id="yzm3l8"
O(log n)
```

---

# How TreeMap Stores Data

Example:

```java id="s2p2du"
map.put(30,"Bob");
```

The key is compared with existing keys.

The tree decides:

* Go left.
* Go right.
* Replace existing value.

---

# TreeMap Requires Ordering

The keys must know how to compare.

There are two options:

1. Comparable.
2. Comparator.

---

# Using Comparable

Example:

```java id="x4u5z9"
class Product implements Comparable<Product>{

    private int id;


    @Override
    public int compareTo(Product other){

        return Integer.compare(
            this.id,
            other.id
        );
    }
}
```

Now TreeMap can sort products.

---

# Using Comparator

More flexible.

Example:

```java id="4p3s6x"
Comparator<Product> comparator =
    (p1,p2) ->
    p1.getName()
       .compareTo(p2.getName());
```

Create:

```java id="8y0v8p"
Map<Product,String> map =
    new TreeMap<>(comparator);
```

---

# Basic TreeMap Operations

The API is the same as other Maps.

---

# Creating

```java id="j8x8xw"
Map<Integer,String> map =
        new TreeMap<>();
```

---

# Adding

```java id="m7j8ko"
map.put(3,"Carlos");
map.put(1,"Alice");
map.put(2,"Bob");
```

Result:

```text id="8o7o0q"
1 → Alice
2 → Bob
3 → Carlos
```

---

# Getting

```java id="j6q7ti"
map.get(2);
```

Returns:

```text id="31s6mk"
Bob
```

---

# Removing

```java id="7m6b9w"
map.remove(1);
```

---

# Iterating

```java id="g7y8u4"
for(Map.Entry<Integer,String> entry :
        map.entrySet()){

    System.out.println(
        entry.getKey()
    );
}
```

Output:

```text id="6n5r1m"
Sorted keys
```

---

# Sorted Map Operations

TreeMap provides additional methods.

These are not available in HashMap.

---

# firstKey()

Returns smallest key:

```java id="8frh4p"
map.firstKey();
```

Example:

```text id="c4z9cw"
10
20
30
```

Returns:

```text id="k1r2hy"
10
```

---

# lastKey()

Returns largest key:

```java id="5y0xqp"
map.lastKey();
```

Returns:

```text id="0f8w8d"
30
```

---

# higherKey()

Finds next greater key.

Example:

Keys:

```text id="m7k8h1"
10
20
30
```

Code:

```java id="w3a6kl"
map.higherKey(20);
```

Result:

```text id="k3b4e7"
30
```

---

# lowerKey()

Finds previous smaller key.

```java id="8h2c5d"
map.lowerKey(20);
```

Result:

```text id="w0h4i7"
10
```

---

# Time Complexity

Because TreeMap uses a balanced tree:

| Operation   | Complexity |
| ----------- | ---------- |
| put         | O(log n)   |
| get         | O(log n)   |
| remove      | O(log n)   |
| containsKey | O(log n)   |

---

# HashMap vs TreeMap Performance

Example:

Search 1 million entries.

---

HashMap:

```text id="q6m7g3"
Average:

O(1)
```

---

TreeMap:

```text id="f8y4e6"
O(log n)
```

HashMap is faster.

But TreeMap provides sorting.

---

# Memory Considerations

TreeMap entries contain:

* Key.
* Value.
* Tree references.

Conceptually:

```text id="q9k4up"
Entry

Key
Value
Left
Right
Parent
Color
```

More memory than HashMap.

---

# TreeMap vs HashMap

| Feature         | HashMap         | TreeMap        |
| --------------- | --------------- | -------------- |
| Ordering        | None            | Sorted         |
| Structure       | Hash table      | Red-Black Tree |
| get             | O(1) avg        | O(log n)       |
| Memory          | Lower           | Higher         |
| Key requirement | hashCode/equals | comparison     |

---

# TreeMap vs LinkedHashMap

| Feature   | LinkedHashMap    | TreeMap     |
| --------- | ---------------- | ----------- |
| Order     | Insertion        | Sorted      |
| Speed     | Faster           | Slower      |
| Structure | Hash + list      | Tree        |
| Use       | Preserve history | Sorted data |

---

# When Should You Use TreeMap?

Use when:

## 1. Keys must stay sorted

Example:

```text id="e4l9om"
Date → Events
```

---

## 2. You need range operations

Example:

Find:

```text id="k5j1uw"
Scores between 500 and 1000
```

---

## 3. You need first/last elements

Example:

```text id="qf0j9x"
Lowest price
Highest price
```

---

# When Should You NOT Use TreeMap?

Avoid when:

## You only need fast lookup

Use:

```java id="tq7b4j"
HashMap
```

---

## You need insertion order

Use:

```java id="69m3dc"
LinkedHashMap
```

---

## You don't need sorting

TreeMap adds unnecessary overhead.

---

# Practical Example — Product Price Catalog

Requirement:

Display products sorted by price.

Data:

```text id="g7x6g1"
100 → Mouse
50 → Keyboard
200 → Monitor
```

TreeMap:

```java id="7h4v8s"
Map<Integer,Product> products =
        new TreeMap<>();
```

Result:

```text id="pf6g2w"
50 → Keyboard
100 → Mouse
200 → Monitor
```

The sorting happens automatically.

---

# Common Mistakes

## Mistake 1 — Expecting insertion order

Wrong:

```text id="8p4c7v"
TreeMap remembers insertion
```

Correct:

```text id="x0f8gj"
TreeMap sorts keys
```

---

## Mistake 2 — Using objects without comparison

Example:

```java id="j4d8w2"
TreeMap<Product,String>
```

without:

* Comparable
* Comparator

will fail.

---

## Mistake 3 — Using TreeMap for everything

Many developers choose it because it "looks organized".

But if you do not need ordering:

```java id="r2q0x5"
HashMap
```

is usually better.

---

# Chapter Summary

You learned:

* `TreeMap` stores keys in sorted order.
* It uses a Red-Black Tree internally.
* Operations are O(log n).
* It requires key comparison.
* It provides useful sorted operations:

  * `firstKey()`
  * `lastKey()`
  * `higherKey()`
  * `lowerKey()`
* It is slower than HashMap but provides ordering.

The key idea:

> HashMap finds things quickly. TreeMap keeps things organized.

---

# ✔️ Next Step

In **Chapter 19 — Comparing HashMap, LinkedHashMap, and TreeMap**, we will consolidate the entire Map family. You will learn how to choose the correct Map implementation based on performance, ordering requirements, and real-world scenarios.
