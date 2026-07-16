# Chapter 15 — Map Interface Introduction

Until now, we studied collections that store individual elements:

* `List`
* `Set`
* `Queue`
* `Deque`

All of them follow the same idea:

> Store a group of objects.

But many real-world problems are not about storing isolated values.

They are about relationships.

Examples:

* User ID → User information.
* Product code → Product.
* Country → Capital.
* Username → Password hash.
* ISBN → Book.

For these situations, Java provides:

```java
Map
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What a `Map` is.
* Why `Map` exists.
* Difference between `Collection` and `Map`.
* Key-value relationships.
* Map hierarchy.
* How keys and values work.
* Basic Map operations.
* When to use Map.

---

# What is a Map?

A `Map` stores data in pairs:

```text
Key → Value
```

Example:

```text id="3y5u8c"
1001 → John
1002 → Maria
1003 → Carlos
```

The key identifies the value.

---

# Real-World Analogy

Think about a dictionary.

You search:

```text id="4x6f6h"
Word → Definition
```

Example:

```text id="q9kq74"
"Java"

↓

Programming language
```

The word is the:

```text id="b7wj2p"
Key
```

The explanation is the:

```text id="f7q5dy"
Value
```

---

# Why Does Map Exist?

Imagine a product system.

You have:

```text id="5h9fmo"
Product 1
Product 2
Product 3
```

A List:

```java
List<Product> products;
```

requires searching:

```java
for(Product p : products){

    if(p.getId() == 100){

    }

}
```

Complexity:

```text id="2vbyj8"
O(n)
```

---

With a Map:

```text id="0o7vpa"
100 → Laptop
101 → Keyboard
102 → Mouse
```

Search:

```java
products.get(100);
```

Much faster.

---

# Map Is Not a Collection

This is a very important concept.

The hierarchy:

```text id="u9b7c1"
Collection
    |
    +-- List
    |
    +-- Set
    |
    +-- Queue
```

But:

```text id="cb3y4p"
Map
```

is separate.

---

# Why?

Because `Collection` stores:

```text id="2o6j0r"
Element
Element
Element
```

Example:

```text id="b1k4a2"
Alice
Bob
Charlie
```

---

A Map stores:

```text id="0k2h3n"
Key → Value
```

Example:

```text id="4u0f7x"
ID → User
```

The structure is fundamentally different.

---

# Map Hierarchy

The main hierarchy:

```text id="9c4m6w"
              Map
               |
      ---------------------
      |          |        |
   HashMap  LinkedHashMap TreeMap
```

These are the main implementations we will study.

---

# Map Components

A Map contains:

## Keys

Identifiers.

Example:

```text id="2om1j5"
1001
1002
1003
```

---

## Values

Associated data.

Example:

```text id="2ed4fv"
John
Maria
Carlos
```

---

Together:

```text id="x58b0n"
1001 → John
1002 → Maria
1003 → Carlos
```

---

# Important Rules

## Rule 1 — Keys are unique

Example:

```text id="axz2h5"
1001 → John
1001 → Maria
```

Impossible.

The second value replaces the first.

Result:

```text id="45u5qk"
1001 → Maria
```

---

## Rule 2 — Values can repeat

Example:

```text id="g1i9jv"
John → Java
Maria → Java
Carlos → Java
```

Allowed.

---

# Creating a Map

The common style:

```java id="2iz6mz"
Map<Integer, String> users =
        new HashMap<>();
```

Meaning:

Key:

```java id="4o9w1f"
Integer
```

Value:

```java id="2bdcsy"
String
```

---

# Adding Elements

Use:

```java id="40k2o9"
put()
```

Example:

```java id="2ow8kj"
users.put(1, "Alice");
users.put(2, "Bob");
users.put(3, "Carlos");
```

Result:

```text id="q8z6pf"
1 → Alice
2 → Bob
3 → Carlos
```

---

# Updating Values

Adding an existing key updates the value.

Example:

```java id="m0f2af"
users.put(1, "Maria");
```

Before:

```text id="7v4v5h"
1 → Alice
```

After:

```text id="3d2j5y"
1 → Maria
```

The key remains.

---

# Getting Values

Use:

```java id="2cx0jv"
get()
```

Example:

```java id="p1m6c9"
String name = users.get(1);
```

Result:

```text id="d4t7un"
Maria
```

---

# Removing Entries

Use:

```java id="4z8x8g"
remove()
```

Example:

```java id="bh4q9y"
users.remove(2);
```

Removes:

```text id="93j5ik"
2 → Bob
```

---

# Checking Keys

Use:

```java id="7ok6ji"
containsKey()
```

Example:

```java id="8x6d7v"
users.containsKey(1);
```

Result:

```text id="ld2w5f"
true
```

---

# Checking Values

Use:

```java id="4t9y6n"
containsValue()
```

Example:

```java
users.containsValue("Maria");
```

---

# Size

```java id="2hj1vw"
users.size();
```

Returns:

```text id="n1e3pn"
number of entries
```

---

# Iterating a Map

A Map is not a Collection, so:

This does not work:

```java id="m5x8rh"
for(String user : map)
```

Because there is no single element.

A Map contains:

```text id="k2qv5p"
Key + Value
```

---

# entrySet()

The most common way:

```java id="u9v4qx"
for(Map.Entry<Integer,String> entry : users.entrySet()){

    System.out.println(
        entry.getKey()
    );

    System.out.println(
        entry.getValue()
    );
}
```

---

Conceptually:

```text id="l8z7a0"
Entry

Key
 |
Value
```

---

# keySet()

Get only keys:

```java id="i2v4yu"
for(Integer key : users.keySet()){

}
```

Example:

```text id="1
2
3
```

---

# values()

Get only values:

```java id="mln9n2"
for(String value : users.values()){

}
```

Example:

```text id="l9f7s8"
Alice
Bob
Carlos
```

---

# Map vs List

Comparison:

| Feature          | List           | Map          |
| ---------------- | -------------- | ------------ |
| Stores           | Elements       | Key-value    |
| Access           | Index          | Key          |
| Duplicate values | Allowed        | Allowed      |
| Duplicate keys   | Not applicable | Not allowed  |
| Search           | Usually O(n)   | Often faster |

---

# Map vs Set

A Set stores:

```text id="8l3m6h"
Unique values
```

Example:

```text id="e1f8ba"
Alice
Bob
Carlos
```

---

Map stores:

```text id="2a7z6h"
Identifier → Data
```

Example:

```text id="v4a7o8"
ID → User
```

---

# Internal Structure Preview

Different Maps use different structures.

---

## HashMap

Uses:

```text id="w9r0l7"
Hash table
```

Similar idea to HashSet.

---

## LinkedHashMap

Uses:

```text id="g0j4ry"
Hash table + linked list
```

Maintains insertion order.

---

## TreeMap

Uses:

```text id="7c1p4m"
Balanced tree
```

Keeps keys sorted.

---

# Memory Considerations

A Map stores more information than a Set.

Set:

```text id="xg0d5p"
Value
```

Map:

```text id="z5h8kq"
Key
Value
Relationship
```

Each entry needs both objects.

---

# Advantages of Map

## 1. Fast Lookup By Identifier

Example:

```java id="y5l6nt"
users.get(id);
```

---

## 2. Represents Relationships Naturally

Examples:

* ID → Object
* Username → Profile
* Code → Description

---

## 3. Flexible

Different implementations provide:

* speed,
* order,
* sorting.

---

# Disadvantages of Map

## 1. More Memory

Stores keys and values.

---

## 2. No Direct Duplicate Keys

Keys must be unique.

---

## 3. Choosing Wrong Implementation

Example:

Need sorted keys but use HashMap.

---

# When Should You Use Map?

Use when:

✅ You need to find something by an identifier.

Examples:

* Database IDs.
* Product codes.
* Usernames.
* Configuration values.

---

# When Should You NOT Use Map?

Avoid when:

❌ You only need a sequence.

Use:

```java
List
```

---

❌ You only need unique values.

Use:

```java
Set
```

---

❌ You only need processing order.

Use:

```java
Queue
```

---

# Practical Example — Product Inventory

Without Map:

```text id="g7q2e8"
Search product:

Product 1
Product 2
Product 3
...
```

With Map:

```java id="6z0p7n"
Map<Integer, Product> inventory;
```

Data:

```text id="q0p7i6"
100 → Notebook
101 → Mouse
102 → Keyboard
```

Search:

```java id="i5d8bk"
inventory.get(101);
```

Result:

```text id="a6t0lm"
Mouse
```

---

# Common Mistakes

## Mistake 1 — Thinking Map extends Collection

It does not.

---

## Mistake 2 — Using duplicate keys expecting multiple values

Example:

```java id="7w0i6p"
map.put(1,"A");
map.put(1,"B");
```

Result:

```text id="9x7j2q"
1 → B
```

---

## Mistake 3 — Assuming HashMap has order

It does not guarantee:

* insertion order,
* sorted order.

---

# Chapter Summary

You learned:

* `Map` stores key-value relationships.
* It is separate from the Collection hierarchy.
* Keys are unique.
* Values can repeat.
* Main operations:

  * `put`
  * `get`
  * `remove`
  * `containsKey`
* Main implementations:

  * `HashMap`
  * `LinkedHashMap`
  * `TreeMap`

The key idea:

> Collections store things; Maps connect things.

---

# ✔️ Next Step

In **Chapter 16 — HashMap**, we will study the most important Map implementation in Java. You will learn how hashing works with keys, how values are located internally, why `hashCode()` and `equals()` are critical, and why `HashMap` is one of the most used classes in professional Java development.
