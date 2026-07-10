# Chapter 09 — StringBuffer and Thread Safety

## Chapter Objective

By the end of this chapter, you should understand:

* What `StringBuffer` is
* Why it was created
* The difference between `StringBuilder` and `StringBuffer`
* What thread safety means
* Why synchronization matters
* When to use StringBuffer
* Why StringBuilder is usually preferred in modern Java applications

---

# 1. The Problem StringBuffer Solves

Before understanding `StringBuffer`, remember:

`String`:

```java id="m0rj2f"
String text = "Java";
```

is immutable.

Every modification creates a new object.

For repeated changes:

```java id="d5y8qk"
text += " Programming";
```

this can become inefficient.

Java introduced mutable text classes:

* `StringBuilder`
* `StringBuffer`

Both allow changing text without creating a new String every time.

---

# 2. What is StringBuffer?

## Definition

`StringBuffer` is a mutable sequence of characters.

Similar to:

```java id="k3y6j9"
StringBuilder
```

Example:

```java id="q4y8v3"
StringBuffer buffer =
    new StringBuffer();

buffer.append("Java");

buffer.append(" Programming");

System.out.println(buffer);
```

Output:

```text id="q6w0bk"
Java Programming
```

---

Internally:

Before:

```text id="4h2b8q"
[]
```

After:

```text id="w4g4mv"
[Java Programming]
```

The same object changes.

---

# 3. Why Does StringBuffer Exist?

The difference is related to:

> Multiple threads accessing the same object.

To understand this, we need to understand threads.

---

# 4. What is a Thread?

A thread is an independent path of execution inside a program.

A simple Java program:

```java id="o1x7o9"
public static void main(String[] args){

}
```

runs on one thread.

But applications can have many:

Example:

```text id="m6z7gc"
Application

Thread 1:
Save user data


Thread 2:
Generate report


Thread 3:
Send notification
```

Multiple things happen at the same time.

---

# 5. The Problem With Shared Data

Imagine:

```java id="a6xj4q"
StringBuilder builder =
    new StringBuilder();
```

Two threads use the same object.

---

Thread A:

```java id="m8qv0s"
builder.append("Hello");
```

Thread B:

```java id="e8a7ut"
builder.append("World");
```

Because both modify the same object, the result can become unpredictable.

Possible:

```text id="f5t7i3"
HelloWorld
```

or:

```text id="x1j7p4"
WorldHello
```

or even corrupted data in certain situations.

---

# 6. What is Thread Safety?

Thread safety means:

> Code behaves correctly when accessed by multiple threads simultaneously.

A thread-safe object controls access so operations do not interfere with each other.

---

# 7. How StringBuffer Provides Thread Safety

StringBuffer methods are synchronized.

Example:

```java id="xj8qv1"
buffer.append("Java");
```

Conceptually:

```text id="n7x0l8"
Thread A
   |
   v
Lock object

append()


Thread B
   |
   waits
```

Only one thread modifies the object at a time.

---

This prevents conflicts.

---

# 8. StringBuilder vs StringBuffer

Comparison:

| Feature         | StringBuilder | StringBuffer |
| --------------- | ------------- | ------------ |
| Mutable         | Yes           | Yes          |
| Thread safe     | No            | Yes          |
| Synchronization | No            | Yes          |
| Performance     | Faster        | Slower       |
| Created         | Java 5        | Java 1.0     |
| Modern usage    | Very common   | Less common  |

---

# 9. Performance Difference

Because StringBuffer synchronizes methods:

Example:

```java id="5q0qzq"
buffer.append("Java");
```

has additional overhead.

Conceptually:

StringBuilder:

```text id="f5k5g0"
append()
 |
 v
modify object
```

---

StringBuffer:

```text id="v6n8h0"
append()
 |
 v
lock object
 |
 v
modify object
 |
 v
release lock
```

---

For single-threaded applications:

StringBuilder is faster.

---

# 10. When Should You Use StringBuffer?

Use StringBuffer when:

* Multiple threads modify the same text object
* Thread safety is required
* Synchronization is important

Example:

A shared logging system:

```text id="t0g4d7"
Thread 1 --->+
              |
Thread 2 ---> | StringBuffer
              |
Thread 3 --->+
```

---

# 11. When Should You Use StringBuilder?

Most of the time.

Examples:

## Generating reports

```java id="l2c8b4"
StringBuilder report =
    new StringBuilder();
```

---

## Building messages

```java id="f4x3l1"
StringBuilder message =
    new StringBuilder();
```

---

## Processing user text

```java id="x7n9q2"
StringBuilder text =
    new StringBuilder();
```

---

Because most console applications:

* have one execution flow
* do not share mutable objects between threads

---

# 12. Example Comparison

## StringBuilder

```java id="1r5d6x"
public class Main {

    public static void main(String[] args) {

        StringBuilder builder =
            new StringBuilder();


        builder.append("Java");

        builder.append(" Bootcamp");


        System.out.println(builder);

    }
}
```

Output:

```text id="6z2o8p"
Java Bootcamp
```

---

## StringBuffer

```java id="2y8s1r"
public class Main {

    public static void main(String[] args) {

        StringBuffer buffer =
            new StringBuffer();


        buffer.append("Java");

        buffer.append(" Bootcamp");


        System.out.println(buffer);

    }
}
```

Output:

```text id="z3s7mm"
Java Bootcamp
```

Same result.

Different internal behavior.

---

# 13. Important: StringBuffer Does Not Replace String

Incorrect thinking:

> "StringBuffer is a better String."

No.

They have different purposes.

---

Use:

```text id="q8y1d5"
String
```

for:

* fixed text
* constants
* values that do not change

Example:

```java id="3m5f5m"
String country = "Brazil";
```

---

Use:

```text id="7n4f1c"
StringBuilder
```

for:

* repeated modifications
* building text

Example:

```java id="7z7c9m"
StringBuilder report;
```

---

Use:

```text id="s8k4w2"
StringBuffer
```

for:

* shared mutable text in multithreaded environments

---

# 14. Common Mistakes

---

## Mistake 1 — Using StringBuffer everywhere

Example:

```java id="4k0v1w"
StringBuffer name =
    new StringBuffer("Java");
```

Not necessary.

If only one thread exists:

Use:

```java id="2jv5e7"
StringBuilder
```

---

## Mistake 2 — Thinking StringBuilder is unsafe always

StringBuilder is unsafe only when:

* multiple threads
* same object
* simultaneous modification

For normal applications:

It is perfectly fine.

---

## Mistake 3 — Using mutable objects unnecessarily

Example:

```java id="8h0c3v"
StringBuilder username =
    new StringBuilder("admin");
```

If the username never changes:

Use:

```java id="a4n7h2"
String username = "admin";
```

---

# 15. Practical Example — Shared Log Builder

Imagine a server:

```text id="j3z0p8"
User request 1
User request 2
User request 3
```

Several threads write logs.

A shared buffer:

```java id="8r4p2d"
StringBuffer logs =
    new StringBuffer();
```

ensures:

```text id="v6r9l1"
Thread 1:
append()

Thread 2:
append()

Thread 3:
append()
```

do not corrupt the result.

---

# 16. Relation to Our Final Project

Our Text Processing Toolkit:

```text id="8w2k0h"
Console application
Single execution flow
```

Therefore:

Preferred:

```java id="8m0z6x"
StringBuilder
```

For:

* reports
* formatted output
* generated summaries

We do not need:

```java id="8n1m2f"
StringBuffer
```

because we are not sharing text between threads.

---

# Chapter Summary

Today we learned:

✅ StringBuffer is mutable
✅ StringBuffer and StringBuilder solve the same general problem
✅ StringBuffer is synchronized
✅ Synchronization provides thread safety
✅ Thread safety has a performance cost
✅ StringBuilder is usually preferred
✅ StringBuffer is useful when multiple threads share the same object

---

# Key Mental Model

Remember:

```text
String:

Immutable
Safe sharing


StringBuilder:

Mutable
Fast
Single thread


StringBuffer:

Mutable
Thread-safe
Multiple threads
```

---

# ✔️ Next Step

Proceed to:

# Chapter 10 — Practical Exercises: Palindrome Checker

Next we will begin applying everything learned so far.

We will build the first real String-processing application:

## Palindrome Checker

Using:

* `String`
* `charAt()`
* `length()`
* `equals()`
* `StringBuilder`
* text normalization techniques

We will develop it step-by-step without providing the complete solution upfront.
