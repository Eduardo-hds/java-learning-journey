# Chapter 07 — HashSet

`HashSet` is the most commonly used implementation of the `Set` interface.

When developers say:

> "I need a collection that does not allow duplicates."

The first solution that usually comes to mind is:

```java
HashSet
```

However, understanding **why** `HashSet` is fast and **how** it prevents duplicates is much more important than memorizing its methods.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `HashSet` is.
* Why it exists.
* How hashing works conceptually.
* How elements are stored internally.
* The relationship between `hashCode()` and `equals()`.
* Performance characteristics.
* Memory considerations.
* When to use and avoid `HashSet`.

---

# What is HashSet?

`HashSet` is a collection that:

* stores unique elements,
* does not guarantee order,
* uses hashing internally,
* provides fast lookup operations.

Example:

```java
Set<String> names = new HashSet<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Conceptually:

```text
HashSet

Alice
Bob
Charlie
```

The order is not guaranteed.

---

# Why Does HashSet Exist?

Imagine storing millions of registered users.

You need to answer:

> "Does this user already exist?"

A `List` would search one by one:

```text
User 1
User 2
User 3
...
User 1000000
```

Complexity:

```text
O(n)
```

For large data, this becomes expensive.

A `HashSet` uses hashing to find elements much faster.

Average complexity:

```text
O(1)
```

---

# The Concept of Hashing

Hashing is a technique that converts an object into a number.

Example:

```text
Object

"Eduardo"

        |
        v

hashCode()

        |
        v

123456
```

This number helps Java decide where to store the element.

---

# Internal Structure (Conceptual)

A `HashSet` is based on a hash table.

Think of it as a collection of buckets.

Example:

```text
Bucket 0
[ ]

Bucket 1
[ Alice ]

Bucket 2
[ ]

Bucket 3
[ Bob ]

Bucket 4
[ Charlie ]
```

The hash code determines the bucket.

Conceptually:

```text
hashCode()

        ↓

calculate position

        ↓

store in bucket
```

---

# Adding an Element

Example:

```java
set.add("Alice");
```

What happens internally?

---

## Step 1 — Calculate hash

Java calls:

```java
hashCode()
```

Example:

```text
"Alice"

↓

12345
```

---

## Step 2 — Find bucket

The hash is converted into a position.

Example:

```text
12345

↓

Bucket 3
```

---

## Step 3 — Check duplicates

If the bucket already contains something, Java checks:

```java
equals()
```

Example:

```text
Existing object.equals(new object)
```

If true:

Duplicate.

The new element is rejected.

---

# hashCode() and equals()

This is one of the most important concepts in Java collections.

Especially for:

* HashSet
* HashMap

---

# The Contract

Java requires:

If two objects are equal:

```java
equals() == true
```

they must have:

```java
same hashCode()
```

Example:

```java
Student("Alice")
```

and

```java
Student("Alice")
```

If they are considered equal:

```text
equals()

true
```

Their hashes must match.

---

# Incorrect Example

```java
class Student {

    private String name;

}
```

Two students:

```java
Student s1 = new Student("Alice");
Student s2 = new Student("Alice");
```

Without overriding:

```java
equals()
hashCode()
```

Java sees:

```text
Different objects
Different references
```

Result:

```text
Set contains two Alices
```

---

# Correct Approach

Override:

```java
equals()
```

and

```java
hashCode()
```

Example:

```java
@Override
public boolean equals(Object o) {

    Student student = (Student) o;

    return name.equals(student.name);
}


@Override
public int hashCode() {

    return name.hashCode();

}
```

Now:

```text
Same name

↓

Same student

↓

Duplicate prevented
```

---

# Basic Operations

## Adding

```java
Set<Integer> numbers = new HashSet<>();

numbers.add(10);
numbers.add(20);
numbers.add(30);
```

---

## Duplicate Addition

```java
numbers.add(10);
```

Nothing changes.

Result:

```text
[10,20,30]
```

---

## Removing

```java
numbers.remove(20);
```

Result:

```text
[10,30]
```

---

## Checking Existence

```java
numbers.contains(30);
```

Returns:

```text
true
```

---

## Size

```java
numbers.size();
```

Returns:

```text
2
```

---

# Iterating Through HashSet

Because there is no index:

Invalid:

```java
set.get(0);
```

Use:

```java
for(String name : names){

    System.out.println(name);

}
```

Example output:

```text
Bob
Alice
Charlie
```

The order may change.

---

# Ordering Behavior

A very important rule:

`HashSet` does not guarantee:

* insertion order,
* sorted order.

Example:

```java
Set<String> names = new HashSet<>();

names.add("A");
names.add("B");
names.add("C");
```

You might see:

```text
C
A
B
```

or:

```text
B
C
A
```

Both are valid.

---

# Time Complexity

Average case:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(1)       |
| remove    | O(1)       |
| contains  | O(1)       |
| size      | O(1)       |

Worst case:

```text
O(n)
```

This happens when many elements collide into the same bucket.

---

# Hash Collision

A collision occurs when different objects produce the same hash position.

Example:

```text
Object A

hash

↓

Bucket 5


Object B

hash

↓

Bucket 5
```

Both go to the same bucket.

Java handles this using additional comparisons.

Conceptually:

```text
Bucket 5

[A] -> [B] -> [C]
```

Modern Java implementations optimize collision handling internally.

---

# Memory Considerations

HashSet requires more memory than a simple array.

It stores:

* buckets,
* hash information,
* references.

Example:

```text
Array:

[A][B][C]


HashSet:

Bucket
 |
 +--> A

Bucket
 |
 +--> B

Bucket
 |
 +--> C
```

The additional structure provides faster lookup.

---

# Advantages of HashSet

## 1. Fast Lookup

Excellent for:

```java
contains()
```

---

## 2. Automatic Duplicate Prevention

The collection enforces uniqueness.

---

## 3. Simple API

Easy to use.

---

## 4. Scales Well

Works efficiently with large amounts of data.

---

# Disadvantages of HashSet

## 1. No Ordering

You cannot depend on iteration order.

---

## 2. No Index Access

No:

```java
get(0)
```

---

## 3. Requires Correct Equality

Custom objects must implement:

* equals()
* hashCode()

correctly.

---

# When Should You Use HashSet?

Use `HashSet` when:

✅ You need unique elements.

Examples:

* usernames,
* IDs,
* tags,
* permissions.

---

✅ You frequently check existence.

Example:

```java
if(users.contains(user)){
    ...
}
```

---

✅ Order is irrelevant.

---

# When Should You NOT Use HashSet?

Avoid it when:

❌ You need insertion order.

Use:

```java
LinkedHashSet
```

---

❌ You need sorted elements.

Use:

```java
TreeSet
```

---

❌ You need duplicates.

Use:

```java
List
```

---

# Practical Example — Unique Words

Imagine analyzing text:

```text
Java is powerful and Java is popular
```

Using a List:

```text
Java
is
powerful
and
Java
is
popular
```

Duplicates remain.

Using HashSet:

```text
Java
is
powerful
and
popular
```

Perfect.

Example:

```java
Set<String> words = new HashSet<>();

words.add("Java");
words.add("is");
words.add("Java");
```

Result:

```text
Java
is
```

---

# Common Mistakes

## Mistake 1 — Expecting order

Wrong:

```java
HashSet<String> set = new HashSet<>();
```

then assuming:

```text
First inserted = first displayed
```

Not guaranteed.

---

## Mistake 2 — Forgetting equals/hashCode

Especially with:

```java
Set<MyObject>
```

---

## Mistake 3 — Using HashSet for indexed data

Example:

```java
students.get(10);
```

Impossible.

Use `List`.

---

# Chapter Summary

In this chapter, you learned:

* `HashSet` stores unique elements using hashing.
* It uses `hashCode()` and `equals()` to detect duplicates.
* It provides very fast average lookup.
* It does not guarantee ordering.
* Correct equality implementation is essential.
* It is usually the default choice when you need a set.

The key idea:

> HashSet sacrifices ordering to achieve fast uniqueness checks.

---

# ✔️ Next Step

In **Chapter 08 — LinkedHashSet**, we will study the middle ground between `HashSet` and `TreeSet`: a collection that keeps the performance benefits of hashing while also preserving the order in which elements were inserted.
