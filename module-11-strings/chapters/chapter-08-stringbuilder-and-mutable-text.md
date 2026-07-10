# Chapter 08 — StringBuilder and Mutable Text

## Chapter Objective

By the end of this chapter, you should understand:

* Why Java created `StringBuilder`
* The difference between immutable and mutable objects
* Why repeated String modification can be inefficient
* How `StringBuilder` works internally
* How to use:

  * `append()`
  * `insert()`
  * `delete()`
  * `reverse()`
  * `toString()`
* When to use `StringBuilder`
* When NOT to use it
* Performance considerations

---

# 1. The Problem With String Modification

We already learned:

> Strings are immutable.

This means:

```java id="a3rjv8"
String text = "Java";
```

cannot become:

```text id="1q6g49"
Java Programming
```

The original String stays unchanged.

---

Example:

```java id="j9d4bt"
String message = "Hello";

message = message + " World";
```

What happens internally?

Many beginners imagine:

```text id="qux7i8"
"Hello"
      |
      v
"Hello World"
```

But Java actually creates a new String:

```text id="5m6h6v"
Step 1:

message
   |
   v
"Hello"


Step 2:

"Hello"

+

" World"


Step 3:

message
   |
   v
"Hello World"
```

The old object still existed.

---

# 2. The Performance Problem

A single concatenation:

```java id="7p7mzh"
String result = "Java" + " Programming";
```

is completely fine.

The problem appears with repeated modifications.

Example:

```java id="ybwq3a"
String result = "";

for(int i = 0; i < 10000; i++){

    result += i;

}
```

Conceptually:

```text id="p4sw4r"
""

"0"

"01"

"012"

"0123"

...
```

Thousands of objects are created.

Memory:

```text id="5azv2k"
Old Strings

""
"0"
"01"
"012"
"0123"
...
```

Most become garbage.

---

This creates:

* unnecessary memory allocation
* more garbage collection work
* slower execution

---

# 3. The Solution: StringBuilder

## What is StringBuilder?

`StringBuilder` is a mutable object designed for building text efficiently.

Mutable means:

> The object can change without creating a new object every time.

---

Example:

```java id="smn7mh"
StringBuilder builder =
    new StringBuilder();

builder.append("Java");

builder.append(" Programming");
```

Internally:

```text id="p0q5tm"
Same object:

[Java]

append()

[Java Programming]
```

The object changes.

---

# 4. String vs StringBuilder

Comparison:

| String                                    | StringBuilder                     |
| ----------------------------------------- | --------------------------------- |
| Immutable                                 | Mutable                           |
| Every change creates a new object         | Changes happen in the same object |
| Good for fixed text                       | Good for dynamic text             |
| Thread-safe by design                     | Not thread-safe                   |
| Less efficient for repeated modifications | More efficient for building text  |

---

# 5. Creating a StringBuilder

Basic:

```java id="tv1i0r"
StringBuilder builder =
    new StringBuilder();
```

Empty builder.

---

With initial text:

```java id="5t2p2r"
StringBuilder builder =
    new StringBuilder("Java");
```

Contains:

```text id="g0e2j4"
Java
```

---

With capacity:

```java id="4u7cgs"
StringBuilder builder =
    new StringBuilder(100);
```

Creates space for approximately 100 characters.

Useful when you know the expected size.

---

# 6. The `append()` Method

## What is it?

Adds text to the end.

This is the most used StringBuilder method.

---

Example:

```java id="xwqj8p"
StringBuilder builder =
    new StringBuilder();

builder.append("Java");

builder.append(" is");

builder.append(" powerful");


System.out.println(builder);
```

Output:

```text id="t2l0bb"
Java is powerful
```

---

Internally:

Step 1:

```text id="4r1l6j"
[]
```

append:

```text id="6x8qtw"
[Java]
```

append:

```text id="9u4t83"
[Java is]
```

append:

```text id="5ng0tv"
[Java is powerful]
```

Same object.

---

# 7. append() With Different Types

StringBuilder can append many types.

Example:

```java id="czl8wo"
StringBuilder builder =
    new StringBuilder();


builder.append("Age: ");

builder.append(25);


System.out.println(builder);
```

Output:

```text id="ytbyps"
Age: 25
```

---

Other examples:

```java id="y4f0q5"
builder.append(true);

builder.append(10.5);

builder.append('A');
```

---

# 8. The `insert()` Method

## What is it?

Adds text at a specific position.

Syntax:

```java id="2l8x7k"
insert(index, value)
```

---

Example:

```java id="qv1gqz"
StringBuilder builder =
    new StringBuilder("Java");


builder.insert(0, "Hello ");


System.out.println(builder);
```

Output:

```text id="v9twjj"
Hello Java
```

---

Before:

```text id="3u2fyo"
Java
```

Insert at index 0:

```text id="q5k4bj"
Hello Java
```

---

Another example:

```java id="r3e7b9"
StringBuilder builder =
    new StringBuilder("Jva");


builder.insert(1, "a");
```

Result:

```text id="14bh6n"
Java
```

---

# 9. The `delete()` Method

## What is it?

Removes characters from a range.

Syntax:

```java id="t0e0qk"
delete(start, end)
```

Remember:

The end index is exclusive.

---

Example:

```java id="gq7o9m"
StringBuilder builder =
    new StringBuilder("Java Programming");


builder.delete(4, 15);


System.out.println(builder);
```

Indexes:

```text id="s7yq1g"
J a v a   P r o g r a m m i n g

0 1 2 3 4 5...
```

Remove:

```text id="l7f0jw"
Programming
```

Result:

```text id="8v0h2y"
Java 
```

---

# 10. The `reverse()` Method

## What is it?

Reverses the characters.

Example:

```java id="y69l9u"
StringBuilder builder =
    new StringBuilder("Java");


builder.reverse();


System.out.println(builder);
```

Output:

```text id="y99o3k"
avaJ
```

---

Common use:

Palindrome checking.

Example:

```text id="3l7h8x"
level

reverse()

level
```

---

# 11. The `toString()` Method

## What is it?

Converts a StringBuilder into a normal String.

Example:

```java id="y5yqfj"
StringBuilder builder =
    new StringBuilder();


builder.append("Java");


String result =
    builder.toString();
```

Now:

```text id="zv99gp"
result
 |
 v
"Java"
```

---

Why convert?

Because many APIs expect:

```java id="t4hxkj"
String
```

not:

```java id="whp7qh"
StringBuilder
```

---

# 12. Practical Example — Building a Report

Imagine generating:

```text id="32i8fq"
User Report

Name: Eduardo
Age: 25
Status: Active
```

Bad approach:

```java id="b5v3om"
String report = "";

report += "User Report\n";
report += "Name: Eduardo\n";
report += "Age: 25\n";
report += "Status: Active\n";
```

Many objects created.

---

Better:

```java id="5m4t87"
StringBuilder report =
    new StringBuilder();


report.append("User Report\n");

report.append("Name: Eduardo\n");

report.append("Age: 25\n");

report.append("Status: Active\n");


System.out.println(
    report.toString()
);
```

---

# 13. StringBuilder in the Final Project

Our Text Processing Toolkit will generate reports.

Example:

```text id="1l4v9d"
Text Statistics

Characters: 150
Words: 30
Longest word: programming
Shortest word: a
```

This is a perfect use case.

Instead of:

```java id="81mjwi"
String report = "";
```

we use:

```java id="b58r88"
StringBuilder report =
    new StringBuilder();
```

---

# 14. Performance Comparison

## String concatenation

Example:

```java id="x8qg7a"
String text = "";

text += "A";

text += "B";

text += "C";
```

Creates:

```text id="7y0p9b"
""

"A"

"AB"

"ABC"
```

---

## StringBuilder

Example:

```java id="a9b5v1"
StringBuilder text =
    new StringBuilder();


text.append("A");

text.append("B");

text.append("C");
```

Creates:

```text id="1ppj13"
One object:

ABC
```

---

For small text:

Both are fine.

For:

* loops
* reports
* generated content
* large messages

prefer:

```java id="qz2t4y"
StringBuilder
```

---

# 15. When NOT to Use StringBuilder

Do not replace every String with StringBuilder.

Example:

```java id="8f1m6f"
String country = "Brazil";
```

No need.

Why?

Because the text never changes.

Use String:

```java id="x4x1tv"
String country = "Brazil";
```

---

Use StringBuilder when:

```text id="2t8p3r"
Many modifications
+
Building text gradually
```

---

# 16. Common Mistakes

---

## Mistake 1 — Forgetting to call toString()

Example:

```java id="h5xxrw"
StringBuilder builder =
    new StringBuilder("Java");

String text = builder;
```

Does not compile.

Correct:

```java id="kq2bq6"
String text = builder.toString();
```

---

## Mistake 2 — Using StringBuilder for fixed text

Unnecessary:

```java id="y7md2m"
StringBuilder name =
    new StringBuilder("Java");
```

If it never changes:

Use:

```java id="h6yk8s"
String name = "Java";
```

---

## Mistake 3 — Ignoring indexes

Example:

```java id="wh3h7q"
builder.delete(0, 100);
```

If the size is smaller:

Exception may occur.

---

# 17. Practice Exercise — Report Builder

Create:

```text id="y0z8qk"
src/
 └── Main.java
```

Build:

```text id="k1w9m7"
=== User Report ===

Name: Eduardo
Role: Java Developer
Level: Beginner

===================
```

Requirements:

Use only:

```java id="x1a8d9"
StringBuilder
append()
toString()
```

Do not use repeated String concatenation.

---

# Chapter Summary

Today we learned:

✅ String is immutable
✅ StringBuilder is mutable
✅ Repeated String modification creates many objects
✅ StringBuilder changes the same object
✅ `append()` adds text
✅ `insert()` adds text at a position
✅ `delete()` removes text
✅ `reverse()` reverses characters
✅ `toString()` converts back to String
✅ StringBuilder is preferred for dynamic text creation

---

# Key Mental Model

Remember:

```text
String:

"Hello"
   |
   |
change
   |
   v
new object


StringBuilder:

[Hello]
   |
 append()
   |
[Hello World]
```

---

# ✔️ Next Step

Proceed to:

# Chapter 09 — StringBuffer and Thread Safety

Next we will learn:

* Why StringBuffer exists
* The difference between StringBuilder and StringBuffer
* What thread safety means
* When synchronization matters
* Why StringBuilder is usually preferred today.
