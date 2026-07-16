# Chapter 06 — The `Set` Interface

Until now, we focused on **Lists**, where order and position matter.

But many real-world problems are different.

Imagine:

* A list of registered emails.
* A list of unique usernames.
* A collection of visited pages.
* A group of permissions.
* A list of allowed roles.

In these cases, the important question is not:

> "What is the position of this element?"

The important question is:

> "Does this element already exist?"

This is where **`Set`** becomes useful.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What a `Set` is.
* Why `Set` exists.
* The difference between `List` and `Set`.
* How duplicate prevention works conceptually.
* How equality affects sets.
* The characteristics of different `Set` implementations.
* When to use and avoid a `Set`.

---

# What is a Set?

A **Set** is a collection that does **not allow duplicate elements**.

Example:

```java
Set<String> names = new HashSet<>();

names.add("Alice");
names.add("Bob");
names.add("Alice");
```

Result:

```text
Alice
Bob
```

The second `"Alice"` is ignored.

---

# Why Does Set Exist?

Let's imagine a registration system.

You store emails:

```text
john@email.com
mary@email.com
alex@email.com
```

Now someone tries to register:

```text
john@email.com
```

again.

With a normal `List`:

```text
john@email.com
mary@email.com
alex@email.com
john@email.com
```

The duplicate exists.

Now every operation must check manually:

```java
if(!emails.contains(email)){
    emails.add(email);
}
```

This logic appears everywhere.

A `Set` solves this problem by making uniqueness part of its design.

---

# Set Characteristics

A `Set` has different characteristics from a `List`.

---

# 1. No Duplicate Elements

Example:

```java
Set<Integer> numbers = new HashSet<>();

numbers.add(10);
numbers.add(20);
numbers.add(10);
```

Stored:

```text
10
20
```

The duplicate is rejected.

---

# 2. No Index

A `Set` does not have positions.

This is invalid:

```java
set.get(0);
```

Why?

Because a set does not promise an ordering.

There is no:

```text
Index 0
Index 1
Index 2
```

---

# 3. Ordering Depends on Implementation

This is extremely important.

The `Set` interface itself does not guarantee order.

Different implementations behave differently:

| Implementation | Ordering            |
| -------------- | ------------------- |
| HashSet        | No guaranteed order |
| LinkedHashSet  | Insertion order     |
| TreeSet        | Sorted order        |

We will study each one separately.

---

# Set Hierarchy

The structure is:

```text
              Set
               |
       -----------------
       |               |
   HashSet       SortedSet
                       |
                    TreeSet
```

Another important implementation:

```text
LinkedHashSet
```

extends `HashSet` behavior while preserving insertion order.

---

# Creating a Set

Recommended style:

```java
Set<String> names = new HashSet<>();
```

Notice:

Variable type:

```java
Set
```

Implementation:

```java
HashSet
```

This follows:

> Program to interfaces, not implementations.

---

# Common Set Methods

Because `Set` extends `Collection`, it inherits many methods.

---

## add()

Adds an element.

```java
names.add("Alice");
```

---

## remove()

Removes an element.

```java
names.remove("Alice");
```

---

## contains()

Checks existence.

```java
names.contains("Bob");
```

Returns:

```text
true
```

---

## size()

Number of elements:

```java
names.size();
```

---

## clear()

Removes everything:

```java
names.clear();
```

---

# How Does Set Know Something Is Duplicate?

This is one of the most important concepts.

When adding:

```java
set.add(object);
```

Java needs to answer:

> "Does this object already exist?"

For most hash-based sets, Java uses:

* `hashCode()`
* `equals()`

---

# hashCode()

`hashCode()` produces an integer representing the object.

Example:

```text
Alice

hashCode()

↓

123456
```

Java uses this value to quickly locate a possible position.

---

# equals()

After finding possible matches, Java checks:

```java
equals()
```

to determine if objects are really equal.

---

# Example

Imagine:

```java
Student s1 = new Student("Alice");
Student s2 = new Student("Alice");
```

Are they duplicates?

It depends on how `equals()` is implemented.

Without overriding:

```java
equals()
```

Java compares references.

Meaning:

```text
s1 == s2
```

False.

They are different objects.

---

With proper `equals()`:

```text
same name

↓

same student

↓

duplicate
```

The set rejects the second object.

---

# Why This Matters

Whenever you store custom objects in:

* HashSet
* HashMap

you should understand:

* `equals()`
* `hashCode()`

Otherwise, duplicate prevention may not work as expected.

This connects directly with the OOP concepts you learned earlier.

---

# Internal Implementation (Conceptual)

The `Set` interface does not define storage.

Each implementation chooses a different structure.

---

## HashSet

Uses:

```text
Hash table
```

Optimized for:

* fast lookup,
* uniqueness.

---

## LinkedHashSet

Uses:

```text
Hash table + linked structure
```

Provides:

* uniqueness,
* insertion order.

---

## TreeSet

Uses:

```text
Tree structure
```

Provides:

* uniqueness,
* sorted elements.

---

# Set vs List

Let's compare.

| Feature           | List               | Set                   |
| ----------------- | ------------------ | --------------------- |
| Duplicates        | Allowed            | Not allowed           |
| Order             | Usually guaranteed | Depends               |
| Index             | Yes                | No                    |
| Search by element | Depends            | Usually optimized     |
| Main purpose      | Store sequence     | Store unique elements |

---

# Example: Student Registration

Using List:

```java
List<String> emails = new ArrayList<>();

emails.add("a@test.com");
emails.add("a@test.com");
```

Result:

```text
a@test.com
a@test.com
```

---

Using Set:

```java
Set<String> emails = new HashSet<>();

emails.add("a@test.com");
emails.add("a@test.com");
```

Result:

```text
a@test.com
```

The data structure itself enforces the rule.

---

# Time Complexity (Conceptual)

The `Set` interface does not define performance.

It depends on implementation.

Preview:

| Operation | HashSet      | TreeSet  |
| --------- | ------------ | -------- |
| add       | O(1) average | O(log n) |
| remove    | O(1) average | O(log n) |
| contains  | O(1) average | O(log n) |

We will analyze these in detail in the next chapters.

---

# Memory Considerations

Sets usually require more memory than simple arrays because they maintain extra structures:

Examples:

Hash-based:

* hash information,
* buckets.

Tree-based:

* node references,
* ordering information.

The extra memory provides faster and more specialized behavior.

---

# Advantages of Set

* Automatically prevents duplicates.
* Expresses intent clearly.
* Efficient searching in many implementations.
* Useful for uniqueness rules.
* Reduces manual validation code.

---

# Disadvantages of Set

* No index access.
* Ordering may not exist.
* More memory than arrays.
* Choosing the wrong implementation affects behavior.

---

# When Should You Use a Set?

Use `Set` when:

✅ Duplicates are invalid.

Examples:

* usernames,
* emails,
* permissions,
* IDs,
* categories.

---

✅ You need fast membership checks.

Example:

```java
if(users.contains(user)){
    ...
}
```

---

✅ The order is not the primary concern.

---

# When Should You NOT Use a Set?

Avoid `Set` when:

❌ You need duplicates.

Example:

A shopping cart:

```text
Product A
Product A
Product B
```

A customer may buy two of the same item.

---

❌ You need index access.

Example:

```java
items.get(10);
```

Use a `List`.

---

❌ You need insertion order but do not choose the correct implementation.

Use:

```java
LinkedHashSet
```

instead.

---

# Common Mistakes

## Mistake 1 — Expecting insertion order

Example:

```java
HashSet<String> names = new HashSet<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Output order is not guaranteed.

---

## Mistake 2 — Using objects without equals/hashCode

Example:

```java
Set<Student> students = new HashSet<>();
```

If `Student` does not correctly implement equality, duplicates may appear.

---

## Mistake 3 — Thinking Set means sorted

A `Set` is not automatically sorted.

Only:

```java
TreeSet
```

provides ordering.

---

# Practical Example — Unique Visitors

Imagine a website tracking visitors.

You don't care:

* visit order,
* number of visits.

You only care:

> "Which users accessed the site?"

A Set is perfect.

```java
Set<String> visitors = new HashSet<>();

visitors.add("john");
visitors.add("mary");
visitors.add("john");
```

Result:

```text
john
mary
```

---

# Chapter Summary

In this chapter, you learned:

* `Set` represents unique collections.
* Duplicate elements are automatically prevented.
* Sets do not use indexes.
* Ordering depends on implementation.
* Equality and hashing are fundamental concepts.
* `HashSet`, `LinkedHashSet`, and `TreeSet` solve different problems.

The key idea:

> Use a Set when the identity of an element matters more than its position.

---

# ✔️ Next Step

In **Chapter 07 — HashSet**, we will study the most common `Set` implementation. You will learn how hashing works conceptually, how buckets store elements, why `hashCode()` matters, its performance characteristics, and why `HashSet` is usually the default choice for unique collections.
