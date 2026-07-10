# Chapter 07 — Splitting and Joining Text

## Chapter Objective

By the end of this chapter, you should understand:

* How to divide a String into smaller parts
* How `split()` works internally
* How arrays are involved in text processing
* How to combine multiple Strings using `join()`
* Common use cases in real applications
* Performance considerations
* Common mistakes when splitting text

---

# 1. Why Split and Join Text?

Real applications constantly receive structured text.

Examples:

## User input

```text
Eduardo,Java,Developer
```

We may want:

```text
Eduardo
Java
Developer
```

---

## Sentences

Input:

```text
Java is powerful
```

We may want:

```text
Java
is
powerful
```

---

## Data processing

Examples:

* CSV-like information
* tags
* commands
* search terms
* configuration values

Java provides:

```java
split()
```

to separate text.

And:

```java
join()
```

to combine text.

---

# 2. The `split()` Method

## What is it?

`split()` divides a String into multiple pieces.

The result is:

```java
String[]
```

(an array of Strings)

---

Example:

```java id="m3q8h9"
String sentence = "Java is awesome";

String[] words = sentence.split(" ");
```

The separator:

```text
space
```

creates:

```text
[
 "Java",
 "is",
 "awesome"
]
```

---

# 3. Understanding the Result

Code:

```java id="dpx8ma"
public class Main {

    public static void main(String[] args) {

        String text = "Java is awesome";

        String[] parts = text.split(" ");

        for(String part : parts){

            System.out.println(part);

        }

    }
}
```

Output:

```text
Java
is
awesome
```

---

What happened internally:

Original:

```text
Java is awesome
```

Split operation:

```text
"Java" "is" "awesome"
```

Stored as:

```text
Index:

0          1        2

Java      is     awesome
```

---

# 4. Splitting by Different Separators

The separator can be any text.

---

## Example: Comma

Input:

```java id="0c6g2d"
String data = "Java,Python,C++,Go";
```

Code:

```java id="b4xk3g"
String[] languages = data.split(",");
```

Result:

```text
[
 Java,
 Python,
 C++,
 Go
]
```

---

## Example: Dash

```java id="d9krq1"
String date = "2026-07-08";

String[] values = date.split("-");
```

Result:

```text
[
2026,
07,
08
]
```

---

# 5. Using split() With Loops

Common pattern:

```java id="x6m8v4"
String sentence = "Java makes programming easier";

String[] words = sentence.split(" ");

for(String word : words){

    System.out.println(word);

}
```

Output:

```text
Java
makes
programming
easier
```

---

# 6. Important: split() Does Not Modify the Original String

Remember:

Strings are immutable.

Example:

```java id="v9o9g0"
String text = "Java Python";

text.split(" ");
```

The original remains:

```text
Java Python
```

The method returns a new array.

Correct:

```java id="y4c5x8"
String[] result = text.split(" ");
```

---

# 7. The Limit Parameter

`split()` has another version:

```java
split(separator, limit)
```

The limit controls the number of parts.

---

Example:

```java id="7xj8r3"
String text = "A-B-C-D";

String[] values = text.split("-", 2);
```

Result:

```text
[
A,
B-C-D
]
```

---

Why?

Because the maximum number of pieces is:

```text
2
```

---

# 8. Common Mistake — Forgetting Empty Values

Example:

```java id="b6u0zj"
String text = "Java,,Python";

String[] values = text.split(",");
```

Many expect:

```text
Java
(empty)
Python
```

However, trailing empty values may be discarded.

For more control:

```java id="6v3f8q"
split(",", -1)
```

---

Example:

```java id="4u8x2m"
String[] values = text.split(",", -1);
```

Preserves empty sections.

---

# 9. The `join()` Method

## What is it?

`join()` combines multiple Strings into one String.

Syntax:

```java id="v1l2r4"
String.join(separator, elements)
```

---

Example:

```java id="2xg6n8"
String result = String.join(
    "-",
    "Java",
    "Python",
    "Go"
);

System.out.println(result);
```

Output:

```text
Java-Python-Go
```

---

# 10. Joining an Array

Very common:

```java id="v3o8x0"
String[] languages = {
    "Java",
    "Python",
    "Go"
};

String result = String.join(
    ", ",
    languages
);

System.out.println(result);
```

Output:

```text
Java, Python, Go
```

---

# 11. split() and join() Together

These methods often work as a pair.

Example:

Input:

```text
java,python,c++
```

Split:

```java id="u7w6o9"
String[] languages =
    text.split(",");
```

Result:

```text
[
java,
python,
c++
]
```

Process data.

Join:

```java id="d8z5qn"
String result =
    String.join(" | ", languages);
```

Output:

```text
java | python | c++
```

---

# 12. Practical Example — Word Counter Preparation

Later we will build:

```text
Text Statistics
```

To count words:

Input:

```text
Java is powerful
```

We can do:

```java id="mx3n1q"
String[] words = text.split(" ");
```

Now:

```text
words.length
```

gives:

```text
3
```

---

# 13. Practical Example — User Tags

Input:

```text
java,spring,backend
```

Code:

```java id="g7m3qk"
public class Main {

    public static void main(String[] args) {

        String tags = "java,spring,backend";


        String[] values = tags.split(",");


        for(String tag : values){

            System.out.println(tag);

        }

    }
}
```

Output:

```text
java
spring
backend
```

---

# 14. Performance Considerations

## split()

Creates:

* a new array
* multiple new String objects

Example:

```java id="6z8j0h"
String[] words = text.split(" ");
```

Memory:

```text
Original String

+

Array

+

Several String objects
```

---

For normal text:

No problem.

---

For massive text processing:

Consider:

* avoiding unnecessary splits
* processing character by character
* using specialized tools

---

# 15. Common Mistakes

---

## Mistake 1 — Using the wrong separator

Example:

```java id="xygq4p"
String date = "2026/07/08";

date.split("-");
```

No match.

Result:

```text
one element
```

because `-` does not exist.

---

## Mistake 2 — Forgetting the result is an array

Wrong:

```java id="l04m6a"
String words = text.split(" ");
```

Correct:

```java id="0gz9jf"
String[] words = text.split(" ");
```

---

## Mistake 3 — Splitting without cleaning text

Example:

```text
"Java   Python"
```

Splitting by one space:

```java
split(" ")
```

may create empty pieces.

Later we will learn better normalization techniques.

---

# 16. Practice Exercise — Sentence Analyzer

Create:

```text
src/
 └── Main.java
```

Use:

```java
String sentence =
"Java is a powerful programming language";
```

Requirements:

1. Split the sentence into words
2. Print every word
3. Count the number of words
4. Join the words using `" - "`

Expected:

```text
Java
is
a
powerful
programming
language

Words: 6

Java - is - a - powerful - programming - language
```

---

# Chapter Summary

Today we learned:

✅ `split()` divides Strings into pieces
✅ `split()` returns a String array
✅ Separators define where splitting happens
✅ `join()` combines Strings together
✅ Split and join are commonly used together
✅ String operations create new data structures
✅ Text processing often relies on these two methods

---

# Key Mental Model

Think:

```text
split()

String
 |
 v
[String, String, String]
```

and:

```text
join()

[String, String, String]
 |
 v
String
```

---

# ✔️ Next Step

Proceed to:

# Chapter 08 — StringBuilder and Mutable Text

Next we will learn:

* Why String concatenation can be inefficient
* Mutable vs immutable objects
* How `StringBuilder` works internally
* `append()`
* `insert()`
* `delete()`
* `reverse()`
* `toString()`

This chapter introduces the main tool for efficient text construction in Java.
