# Chapter 03 — ArrayList

`ArrayList` is probably the most used collection class in Java applications.

If you ask most Java developers:

> "Which collection do you use most often?"

The answer will usually be:

```java
ArrayList
```

However, using `ArrayList` everywhere without understanding how it works is a common mistake.

The goal of this chapter is not only to learn **how to use it**, but to understand **why it behaves the way it does**.

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `ArrayList` is.
* Why it exists.
* How it works internally.
* How dynamic resizing happens.
* The difference between size and capacity.
* Performance characteristics.
* Memory behavior.
* Advantages and disadvantages.
* When to use and when to avoid `ArrayList`.

---

# What is ArrayList?

`ArrayList` is a resizable implementation of the `List` interface.

It provides:

* ordered elements,
* index-based access,
* duplicate elements,
* dynamic size.

Example:

```java
List<String> names = new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Conceptually:

```text
Index

0        1        2

Alice    Bob      Charlie
```

Just like an array, elements are accessed using indexes.

---

# Why Does ArrayList Exist?

Java already had arrays.

So why create `ArrayList`?

Because arrays have limitations:

```java
String[] names = new String[10];
```

Problems:

* Fixed size.
* Manual resizing.
* Manual element movement.
* No useful manipulation methods.

`ArrayList` solves these problems.

Instead of:

```java
Create bigger array
Copy elements
Replace old array
```

Java handles the process internally.

---

# Internal Implementation

The most important concept:

> `ArrayList` is internally backed by an array.

Conceptually:

```text
ArrayList

        internal array

+----+----+----+----+----+
| A  | B  | C  |    |    |
+----+----+----+----+----+

size = 3
capacity = 5
```

The `ArrayList` is not a completely new storage mechanism.

It is a wrapper around a normal array with extra management logic.

---

# Size vs Capacity

This is one of the most important concepts.

## Size

Number of elements currently stored.

Example:

```java
list.add("Alice");
list.add("Bob");
```

Size:

```
2
```

---

## Capacity

The amount of space currently available internally.

Example:

```text
Capacity = 10

+---+---+---+---+---+---+---+---+---+---+
| A | B |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+

Size = 2
```

The list has room for more elements before needing to resize.

---

# Dynamic Resizing

Imagine:

```java
ArrayList<Integer> numbers = new ArrayList<>();
```

Initially:

```text
Capacity = small internal array
Size = 0
```

Adding elements:

```java
numbers.add(10);
numbers.add(20);
numbers.add(30);
```

Eventually:

```text
Capacity full
```

What happens?

Java creates a larger array.

Example:

Before:

```text
+---+---+---+
|10 |20 |30 |
+---+---+---+
```

New larger array:

```text
+---+---+---+---+---+
|10 |20 |30 |   |   |
+---+---+---+---+---+
```

Then:

1. Copy old elements.
2. Replace internal array.
3. Continue adding.

This process is called **resizing**.

---

# Why Not Resize Every Time?

Imagine adding 1 million elements.

If Java created a new array every single time:

```
add
copy

add
copy

add
copy
```

The performance would be terrible.

Instead, `ArrayList` grows strategically.

It increases capacity in larger steps.

This reduces the number of expensive copy operations.

---

# Creating an ArrayList

The recommended style:

```java
List<String> names = new ArrayList<>();
```

Using the interface:

```java
List
```

allows changing implementations later.

Example:

```java
List<String> names = new LinkedList<>();
```

The rest of the application does not need to change.

---

# Basic Operations

## Adding Elements

At the end:

```java
names.add("Alice");
```

Result:

```text
[Alice]
```

---

Adding multiple:

```java
names.add("Bob");
names.add("Charlie");
```

Result:

```text
[Alice, Bob, Charlie]
```

---

## Adding at a Specific Position

```java
names.add(1, "David");
```

Before:

```text
0 Alice
1 Bob
2 Charlie
```

After:

```text
0 Alice
1 David
2 Bob
3 Charlie
```

Notice:

Elements after index 1 must shift.

---

# Removing Elements

By index:

```java
names.remove(1);
```

Example:

Before:

```text
Alice
Bob
Charlie
```

Remove index 1:

```text
Alice
Charlie
```

The remaining elements shift left.

---

By object:

```java
names.remove("Charlie");
```

Java searches for the element and removes it.

---

# Updating Elements

Using:

```java
set()
```

Example:

```java
names.set(0, "Alex");
```

Before:

```
Alice
Bob
```

After:

```
Alex
Bob
```

The position remains the same.

---

# Searching

## contains()

```java
names.contains("Alice");
```

Returns:

```text
true
```

---

## indexOf()

```java
names.indexOf("Bob");
```

Returns:

```
1
```

If not found:

```
-1
```

---

# Iteration

Enhanced for loop:

```java
for(String name : names){
    System.out.println(name);
}
```

---

Traditional loop:

```java
for(int i = 0; i < names.size(); i++){

    System.out.println(names.get(i));

}
```

The second approach works well because `ArrayList` has fast index access.

---

# Time Complexity

Now we reach one of the most important topics.

Big-O describes how the cost grows as data increases.

---

## Access by Index

Example:

```java
names.get(5000);
```

Complexity:

```
O(1)
```

Why?

Because arrays store elements continuously.

Java can calculate the exact memory position immediately.

---

## Add at End

Example:

```java
names.add("John");
```

Usually:

```
O(1)
```

Very fast.

Exception:

When resizing happens:

```
O(n)
```

because elements must be copied.

---

## Insert in Middle

Example:

```java
names.add(100,"John");
```

Complexity:

```
O(n)
```

Why?

Elements must move.

Example:

Before:

```
A B C D E
```

Insert X:

```
A B X C D E
```

C, D, and E move.

---

## Remove from Middle

Example:

```java
names.remove(100);
```

Complexity:

```
O(n)
```

Because elements shift.

---

## Search

Example:

```java
names.contains("John");
```

Complexity:

```
O(n)
```

Worst case:

Java checks every element.

---

# Memory Considerations

`ArrayList` stores:

* the internal array,
* references to objects,
* size information,
* capacity information.

Example:

```java
List<Student> students = new ArrayList<>();
```

The list does not store the entire object directly.

It stores references:

```text

ArrayList

+--------+
| ref 1  | -----> Student object
| ref 2  | -----> Student object
| ref 3  | -----> Student object
+--------+

```

---

# Advantages of ArrayList

## 1. Fast Random Access

Excellent:

```java
list.get(index);
```

---

## 2. Simple and Flexible

Most business applications benefit from it.

---

## 3. Efficient Memory Usage

Compared with linked structures, it has less overhead.

---

## 4. Great Default Choice

When unsure, `ArrayList` is often the correct starting point.

---

# Disadvantages of ArrayList

## 1. Slow Middle Insertions

Because elements shift.

---

## 2. Slow Removals

Same reason.

---

## 3. Searching Is Linear

Finding an element requires scanning.

---

## 4. Resizing Cost

Occasionally expensive.

---

# When Should You Use ArrayList?

Use `ArrayList` when:

✅ You need indexed access.

Example:

```java
products.get(50);
```

---

✅ Most operations happen at the end.

Example:

Shopping cart:

```
add product
add product
add product
```

---

✅ Reading data is more common than modifying it.

Examples:

* Reports
* Catalogs
* Lists displayed to users

---

# When Should You NOT Use ArrayList?

Avoid it when:

❌ You constantly insert/remove elements in the middle.

Example:

```
Insert at position 0
Remove at position 0
Insert at position 0
```

A `LinkedList` may be better.

---

❌ You need unique elements.

Use:

```
Set
```

---

❌ You need key-based lookup.

Use:

```
Map
```

---

# Common Mistakes

## Mistake 1 — Using ArrayList everywhere

Example:

```java
ArrayList everything = new ArrayList();
```

This ignores the purpose of different collections.

---

## Mistake 2 — Using remove incorrectly

Example:

```java
List<Integer> numbers = new ArrayList<>();

numbers.add(10);
numbers.add(20);

numbers.remove(10);
```

This removes by index, not value.

Because:

```java
remove(int index)
```

has priority.

---

Correct:

```java
numbers.remove(Integer.valueOf(10));
```

---

## Mistake 3 — Assuming capacity equals size

Example:

Capacity:

```
1000
```

Does not mean:

```
1000 elements
```

It means:

```
space available for 1000 elements
```

---

# Practical Example — Student Management

Imagine:

```java
List<Student> students = new ArrayList<>();

students.add(new Student("Alice"));
students.add(new Student("Bob"));
students.add(new Student("Carlos"));
```

Operations:

Add:

```java
students.add(student);
```

Search:

```java
students.contains(student);
```

Remove:

```java
students.remove(student);
```

Display:

```java
for(Student student : students){
    System.out.println(student);
}
```

This is exactly the type of structure we'll use in the Student Management exercise later.

---

# Chapter Summary

In this chapter, you learned:

* `ArrayList` is a dynamic array implementation of `List`.
* Internally, it uses an array.
* It automatically manages resizing.
* Size and capacity are different concepts.
* Index access is extremely fast.
* Insertions and removals in the middle are slower.
* `ArrayList` is the default choice for many applications.

The most important idea:

> `ArrayList` is optimized for fast reading and accessing elements, not frequent structural changes in the middle.

---

# ✔️ Next Step

In **Chapter 04 — LinkedList**, we will study the alternative `List` implementation. You will learn how linked nodes work internally, why insertions can be faster, why random access is slower, and finally we will compare **ArrayList vs LinkedList** in depth.
