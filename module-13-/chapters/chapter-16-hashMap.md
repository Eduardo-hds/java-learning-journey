# Chapter 16 — HashMap

`HashMap` is one of the most important classes in the Java Collections Framework.

In professional Java applications, it appears everywhere:

* Caching data.
* Storing configurations.
* Managing objects by ID.
* Representing relationships.
* Fast lookups.

Examples:

```text
User ID → User
Product Code → Product
Username → Profile
```

The main idea:

> `HashMap` provides fast access to values using keys.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `HashMap` is.
* Why it exists.
* How keys are converted into locations.
* Internal structure.
* The role of `hashCode()` and `equals()`.
* Performance characteristics.
* Memory considerations.
* When to use and avoid `HashMap`.

---

# What is HashMap?

`HashMap` is a `Map` implementation that stores:

```text
Key → Value
```

Example:

```java
Map<Integer, String> users = new HashMap<>();

users.put(1, "Alice");
users.put(2, "Bob");
users.put(3, "Carlos");
```

Conceptually:

```text
1 → Alice
2 → Bob
3 → Carlos
```

---

# Why Does HashMap Exist?

Imagine an application with one million users.

You need:

> Find user by ID.

Using a `List`:

```java
for(User user : users){

    if(user.getId() == id){

    }

}
```

Complexity:

```text
O(n)
```

With a `HashMap`:

```java
users.get(id);
```

Average:

```text
O(1)
```

The key allows direct access.

---

# Internal Structure

A `HashMap` uses a structure similar to `HashSet`.

Conceptually:

```text
Hash Table

Bucket 0

Bucket 1
   |
   +---- Key → Value

Bucket 2

Bucket 3
   |
   +---- Key → Value
```

The key determines where the entry is stored.

---

# How HashMap Stores Data

Example:

```java
map.put("username", "Eduardo");
```

Internally:

---

## Step 1 — Calculate hash

Java calls:

```java
key.hashCode()
```

Example:

```text
"username"

↓

123456
```

---

## Step 2 — Find bucket

The hash is transformed into an internal position.

Example:

```text
123456

↓

Bucket 5
```

---

## Step 3 — Store entry

The entry contains:

```text
Key
Value
Hash
Reference
```

Conceptually:

```text
Bucket 5

+----------------+
| Key            |
| Value          |
| Hash           |
+----------------+
```

---

# Getting a Value

Example:

```java
String name = map.get("username");
```

What happens?

---

## Step 1

Calculate hash:

```text
"username"

↓

123456
```

---

## Step 2

Find bucket.

---

## Step 3

Compare keys.

Java uses:

```java
equals()
```

---

## Step 4

Return value.

```text
Eduardo
```

---

# hashCode() and equals()

This is one of the most important concepts in Java.

Especially for:

* HashMap.
* HashSet.

---

# The Rule

If two keys are considered equal:

```java
equals() == true
```

they must have:

```java
same hashCode()
```

---

# Example Problem

Class:

```java
class Product {

    private int id;

}
```

Without:

```java
equals()
hashCode()
```

Two objects:

```java
Product p1 = new Product(10);
Product p2 = new Product(10);
```

may be considered different keys.

Result:

```text
10 → Product A

10 → Product B
```

The Map cannot identify them correctly.

---

# Correct Implementation

Example:

```java
@Override
public boolean equals(Object obj){

    Product other = (Product) obj;

    return id == other.id;

}


@Override
public int hashCode(){

    return Integer.hashCode(id);

}
```

Now:

```text
Same ID

↓

Same key
```

---

# Basic HashMap Operations

---

# Adding Entries

Use:

```java
put()
```

Example:

```java
Map<Integer, String> users =
        new HashMap<>();

users.put(1, "Alice");
users.put(2, "Bob");
```

Result:

```text
1 → Alice
2 → Bob
```

---

# Updating Values

Same key:

```java
users.put(1, "Maria");
```

Before:

```text
1 → Alice
```

After:

```text
1 → Maria
```

The old value is replaced.

---

# Getting Values

```java
users.get(1);
```

Result:

```text
Maria
```

---

# Removing Entries

```java
users.remove(1);
```

Removes:

```text
1 → Maria
```

---

# Checking Keys

```java
users.containsKey(2);
```

Result:

```text
true
```

---

# Checking Values

```java
users.containsValue("Bob");
```

---

# Iterating HashMap

A Map contains entries.

The preferred approach:

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

---

# keySet()

Only keys:

```java
for(Integer id : users.keySet()){

}
```

Example:

```text
1
2
3
```

---

# values()

Only values:

```java
for(String name : users.values()){

}
```

Example:

```text
Alice
Bob
Carlos
```

---

# Ordering Behavior

Important:

`HashMap` does NOT guarantee order.

Example:

Inserted:

```text
1 → Alice
2 → Bob
3 → Carlos
```

Iteration may produce:

```text
3 → Carlos
1 → Alice
2 → Bob
```

Do not depend on order.

---

# Time Complexity

Average case:

| Operation   | Complexity |
| ----------- | ---------- |
| put         | O(1)       |
| get         | O(1)       |
| remove      | O(1)       |
| containsKey | O(1)       |

---

Worst case:

```text
O(n)
```

This occurs with many collisions.

---

# Hash Collision

A collision happens when different keys map to the same bucket.

Example:

```text
Key A

hash

↓

Bucket 3


Key B

hash

↓

Bucket 3
```

Conceptually:

```text
Bucket 3

Key A → Value A

Key B → Value B
```

Java handles this internally.

---

# Java 8 Improvement

Before Java 8:

Collisions used:

```text
Linked List
```

Example:

```text
A → B → C
```

---

Java 8+ can transform large collision chains into:

```text
Balanced Tree
```

Example:

```text
        B

      /   \

     A     C
```

This improves worst-case performance.

---

# Memory Considerations

A HashMap stores:

* table of buckets,
* keys,
* values,
* entry objects.

Compared with:

```text
List<Value>
```

it uses more memory.

Because it stores:

```text
Key + Value + Structure
```

---

# HashMap vs HashSet

Very important comparison.

Internally:

```text
HashSet
```

is backed by:

```text
HashMap
```

Conceptually:

HashSet:

```text
Value
```

becomes:

```text
Key → Dummy Object
```

Example:

```text
Alice
```

internally:

```text
Alice → PRESENT
```

---

# HashMap vs TreeMap

| Feature   | HashMap     | TreeMap      |
| --------- | ----------- | ------------ |
| Structure | Hash table  | Tree         |
| Ordering  | None        | Sorted keys  |
| get       | O(1) avg    | O(log n)     |
| Memory    | Lower       | Higher       |
| Use       | Fast lookup | Ordered data |

---

# HashMap vs LinkedHashMap

| Feature | HashMap         | LinkedHashMap   |
| ------- | --------------- | --------------- |
| Order   | None            | Insertion order |
| Speed   | Slightly faster | Slightly slower |
| Memory  | Lower           | Higher          |

---

# When Should You Use HashMap?

Use it when:

## 1. You need lookup by key

Examples:

```text
ID → Object
Code → Description
```

---

## 2. Performance matters

Example:

Millions of records.

---

## 3. Order is irrelevant

---

# When Should You NOT Use HashMap?

Avoid when:

## Need sorted keys

Use:

```java
TreeMap
```

---

## Need insertion order

Use:

```java
LinkedHashMap
```

---

## Need only values

Use:

```java
List
```

or:

```java
Set
```

---

# Practical Example — Inventory System

Without Map:

```text
Search product:

100
101
102
...
```

With HashMap:

```java
Map<Integer, Product> inventory;
```

Data:

```text
100 → Notebook
101 → Mouse
102 → Keyboard
```

Search:

```java
inventory.get(101);
```

Result:

```text
Mouse
```

---

# Common Mistakes

## Mistake 1 — Using mutable keys

Bad:

```java
Map<Person, String>
```

where `Person` changes fields used in:

```java
hashCode()
```

The Map may no longer find the key.

---

## Mistake 2 — Assuming order

Wrong:

```text
HashMap remembers insertion order
```

It does not.

---

## Mistake 3 — Forgetting equals/hashCode

Custom objects require correct implementation.

---

## Mistake 4 — Using get() without checking

Example:

```java
map.get(id).getName();
```

If key does not exist:

```text
NullPointerException
```

Better:

```java
if(map.containsKey(id)){
    
}
```

---

# Chapter Summary

You learned:

* `HashMap` stores key-value pairs.
* It uses hashing for fast access.
* Keys determine storage location.
* `hashCode()` and `equals()` are essential.
* Average operations are O(1).
* It does not guarantee order.
* It is one of the most used collections in Java.

The key idea:

> HashMap trades ordering for extremely fast key-based access.

---

# ✔️ Next Step

In **Chapter 17 — LinkedHashMap**, we will study the Map implementation that keeps the performance characteristics of hashing while adding predictable insertion order. You will learn why it is useful for caches, histories, and ordered reports.
