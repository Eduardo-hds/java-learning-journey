# Chapter 02 — Creating Strings and the String Pool

## Chapter Objective

By the end of this chapter, you should understand:

* The different ways to create Strings in Java
* The difference between String literals and `new String()`
* How the String Pool works internally
* How Java saves memory by reusing Strings
* Why String literals are preferred in most situations
* How references and objects behave in memory
* Common mistakes when creating Strings

---

# 1. Creating Strings in Java

There are two main ways to create a String.

## Approach 1 — String Literal

Example:

```java
String language = "Java";
```

This is the most common way.

---

## Approach 2 — Using `new String()`

Example:

```java
String language = new String("Java");
```

Both create a String containing:

```text
Java
```

However, internally they behave differently.

---

# 2. String Literal Creation

When Java sees:

```java
String name = "Java";
```

it does not immediately create a completely new object every time.

Instead, Java checks the **String Pool**.

Conceptually:

```text
String Pool

+---------+
| Java    |
+---------+
```

The variable points to that existing object:

```text
name
 |
 v
"Java"
```

---

Now imagine:

```java
String a = "Java";
String b = "Java";
```

What happens?

Many beginners imagine:

```text
a ---> "Java"

b ---> "Java"
```

Two objects.

But Java can optimize:

```text
       +---------+
a ---->|         |
       |  Java   |
b ---->|         |
       +---------+
```

Both references point to the same String.

---

# 3. What is the String Pool?

The String Pool is a special area where Java stores String literals.

Its purpose:

> Avoid creating duplicate String objects.

Example:

```java
String first = "Java";
String second = "Java";
String third = "Java";
```

Without a pool:

```text
"Java"
"Java"
"Java"
```

Three objects.

With the pool:

```text
          +--------+
first --->|        |
second -->| Java   |
third --->|        |
          +--------+
```

One object.

---

# 4. Why Can Java Safely Share Strings?

Because Strings are immutable.

Imagine this:

```java
String a = "Java";
String b = "Java";
```

Both share:

```text
"Java"
```

Now:

```java
a = "Python";
```

Does not change the original.

It creates a new reference:

Before:

```text
a ----\
       ---> "Java"
b ----/
```

After:

```text
a --------> "Python"

b --------> "Java"
```

The shared object is safe.

---

# 5. Creating Strings with `new String()`

Now consider:

```java
String language = new String("Java");
```

This explicitly creates a new object.

Conceptually:

```text
Heap:

+---------+
| Java    |
+---------+

String Pool:

+---------+
| Java    |
+---------+
```

There may now be two objects containing the same text.

One in:

* String Pool
* Heap memory

---

Example:

```java
String a = "Java";

String b = new String("Java");
```

Memory:

```text
String Pool:

+--------+
| Java   |
+--------+
    ^
    |
    a


Heap:

+--------+
| Java   |
+--------+
    ^
    |
    b
```

The content is equal.

The objects are different.

---

# 6. Comparing Literal and `new String()`

Example:

```java
public class Main {

    public static void main(String[] args) {

        String a = "Java";

        String b = "Java";

        String c = new String("Java");


        System.out.println(a == b);

        System.out.println(a == c);

    }
}
```

Output:

```text
true
false
```

Why?

---

## First comparison

```java
a == b
```

Both point to the same pooled object.

```text
a ----\
       ---> "Java"
b ----/
```

So:

```text
true
```

---

## Second comparison

```java
a == c
```

Different objects.

```text
Pool:

a ---> "Java"


Heap:

c ---> "Java"
```

So:

```text
false
```

---

Important:

The text is the same.

But the objects are different.

For content comparison:

```java
equals()
```

should be used.

Example:

```java
System.out.println(a.equals(c));
```

Result:

```text
true
```

---

# 7. Why Prefer String Literals?

Usually:

```java
String name = "Java";
```

is preferred.

Reasons:

---

## 1. Memory Efficiency

Example:

```java
String a = "Java";
String b = "Java";
String c = "Java";
```

Uses one object.

---

Using:

```java
String a = new String("Java");
String b = new String("Java");
String c = new String("Java");
```

Creates multiple objects.

Memory:

```text
Object 1: Java
Object 2: Java
Object 3: Java
```

Wasteful.

---

## 2. Better Performance

The JVM can quickly reuse pooled Strings.

Less object creation means:

* less memory allocation
* less garbage collection
* better performance

---

## 3. Cleaner Code

Most Java applications use:

```java
String username = "admin";
```

not:

```java
String username = new String("admin");
```

---

# 8. When Would `new String()` Be Used?

Rarely.

Usually only when you specifically need a different object.

Example:

```java
String a = "Java";

String b = new String(a);
```

Now:

```text
a != b
```

because they are different objects.

However, this is uncommon in normal applications.

---

# 9. The `intern()` Method

Java provides:

```java
intern()
```

which allows moving a String reference into the String Pool.

Example:

```java
String a = new String("Java");

String b = a.intern();
```

Conceptually:

Before:

```text
Heap:

a ---> "Java"
```

After:

```text
Pool:

b ---> "Java"
```

Now:

```java
System.out.println(b == "Java");
```

returns:

```text
true
```

---

However:

You usually do not need to call `intern()` manually.

The JVM already handles most cases efficiently.

---

# 10. Important Memory Model

Let's summarize.

## Literal

Code:

```java
String a = "Java";
```

Memory:

```text
String Pool

+--------+
| Java   |
+--------+

a ------>
```

---

## new String()

Code:

```java
String b = new String("Java");
```

Memory:

```text
String Pool

+--------+
| Java   |
+--------+


Heap

+--------+
| Java   |
+--------+

b ------>
```

---

# 11. Common Mistakes

---

## Mistake 1 — Using `new String()` everywhere

Bad:

```java
String name = new String("Eduardo");
```

Better:

```java
String name = "Eduardo";
```

---

## Mistake 2 — Thinking identical text means identical objects

Example:

```java
String a = new String("Java");
String b = new String("Java");
```

Many think:

```java
a == b
```

is true.

It is false.

They have different references.

---

## Mistake 3 — Using `==` for String comparison

Wrong:

```java
if(username == "admin")
```

Correct:

```java
if(username.equals("admin"))
```

We will explore this deeply later.

---

# 12. Practical Experiment

Create:

```text
src/
 └── Main.java
```

Code:

```java
public class Main {

    public static void main(String[] args) {

        String first = "Java";

        String second = "Java";

        String third = new String("Java");


        System.out.println(first == second);

        System.out.println(first == third);

        System.out.println(first.equals(third));

    }
}
```

Expected output:

```text
true
false
true
```

---

# Chapter Summary

Today we learned:

✅ Strings can be created using literals or `new String()`
✅ String literals are stored in the String Pool
✅ The JVM reuses identical literals
✅ Immutability makes sharing safe
✅ `new String()` creates a separate object
✅ `==` compares references
✅ `equals()` compares content
✅ String literals are preferred in normal applications

---

# Key Mental Model

Remember:

```text
String Pool stores reusable Strings.

String literals use the pool.

new String() creates a new object.

Same text ≠ same object.
```

---

# ✔️ Next Step

Proceed to:

# Chapter 03 — Basic String Inspection

Next we will start using the String API:

* `length()`
* `isEmpty()`
* `isBlank()`
* `charAt()`

and learn how Java allows us to inspect text safely.
