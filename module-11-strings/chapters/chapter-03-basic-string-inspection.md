# Chapter 03 — Basic String Inspection

## Chapter Objective

By the end of this chapter, you should understand:

* How to inspect String content
* How to determine the size of a String
* The difference between empty and blank text
* How character indexing works
* How Java handles positions inside Strings
* Common mistakes when inspecting text

We will start working with the String API, but always remembering the foundation:

> Strings are immutable objects. Methods that analyze Strings do not change them.

---

# 1. String Methods Overview

A String object contains many built-in methods.

Example:

```java
String name = "Java";

name.length();
```

The method:

```java
length()
```

belongs to the String class.

Conceptually:

```text
String object

+----------------+
| Java           |
+----------------+
        |
        |
        v

     length()
```

Methods allow us to ask questions about text.

Examples:

* How many characters exist?
* Is it empty?
* What character exists at a position?
* Does this text contain something?

---

# 2. The `length()` Method

## What is it?

`length()` returns the number of characters inside a String.

Example:

```java
String language = "Java";

System.out.println(language.length());
```

Output:

```text
4
```

Because:

```text
Index:

0 1 2 3
J a v a
```

There are four characters.

---

# Important: Length is NOT the last index

Many beginners confuse these concepts.

Example:

```java
String word = "Java";
```

Length:

```text
4
```

Indexes:

```text
0 1 2 3
J a v a
```

The last index is:

```text
length - 1
```

Therefore:

```java
word.length() - 1
```

equals:

```text
3
```

---

## Example

```java
public class Main {

    public static void main(String[] args) {

        String text = "Programming";

        System.out.println(text.length());

    }
}
```

Output:

```text
11
```

---

# Internal Behavior

Conceptually, a String stores:

```text
P r o g r a m m i n g
```

Java already knows the size.

Calling:

```java
text.length();
```

does not need to count characters every time.

The String object keeps this information internally.

Performance:

```
O(1)
```

Meaning:

The operation is extremely fast.

---

# 3. The `isEmpty()` Method

## What is it?

`isEmpty()` checks whether a String has zero characters.

Example:

```java
String text = "";

System.out.println(text.isEmpty());
```

Output:

```text
true
```

---

Another example:

```java
String name = "Java";

System.out.println(name.isEmpty());
```

Output:

```text
false
```

Because:

```text
Java
```

contains characters.

---

# Internally

This:

```java
text.isEmpty();
```

is conceptually similar to:

```java
text.length() == 0;
```

Example:

```java
if(text.length() == 0){

}
```

and:

```java
if(text.isEmpty()){

}
```

are equivalent.

However:

```java
isEmpty()
```

is clearer.

---

# When to Use `isEmpty()`

Good:

```java
if(username.isEmpty()){

    System.out.println("Username required");

}
```

Useful for:

* form validation
* input checking
* preventing invalid data

---

# Common Mistake

This:

```java
String text = null;
```

is NOT an empty String.

There is a difference:

Empty:

```java
""
```

Null:

```java
null
```

Example:

```java
String text = null;

text.isEmpty();
```

causes:

```
NullPointerException
```

because there is no object.

---

# 4. The `isBlank()` Method

## What is it?

`isBlank()` checks whether a String contains only whitespace characters.

Examples:

```java
""
```

```java
"   "
```

```java
"      "
```

are considered blank.

---

Example:

```java
String text = "   ";

System.out.println(text.isBlank());
```

Output:

```text
true
```

---

Compare:

```java
String text = "   ";

System.out.println(text.isEmpty());

System.out.println(text.isBlank());
```

Output:

```text
false
true
```

Why?

Because the String has characters:

```
space
space
space
```

Length is not zero.

---

# Empty vs Blank

| Value    | Empty? | Blank? |
| -------- | ------ | ------ |
| `""`     | true   | true   |
| `" "`    | false  | true   |
| `"   "`  | false  | true   |
| `"Java"` | false  | false  |

---

# When to Use `isBlank()`

For user input validation:

Example:

```java
String username = "     ";

if(username.isBlank()){

    System.out.println("Invalid username");

}
```

This prevents users from entering only spaces.

---

# Why Was `isBlank()` Added?

Before Java 11, developers commonly wrote:

```java
text.trim().isEmpty()
```

Example:

```java
if(text.trim().isEmpty()){

}
```

Java introduced:

```java
isBlank()
```

because it expresses the intention better.

---

# 5. The `charAt()` Method

## What is it?

`charAt()` returns a character from a specific position.

Example:

```java
String word = "Java";

System.out.println(word.charAt(0));
```

Output:

```text
J
```

---

Remember indexes start at zero:

```text
Index:

0 1 2 3
J a v a
```

Therefore:

```java
word.charAt(0)
```

returns:

```
J
```

```java
word.charAt(3)
```

returns:

```
a
```

---

# Example

```java
public class Main {

    public static void main(String[] args) {

        String language = "Java";

        char first = language.charAt(0);

        char last = language.charAt(3);

        System.out.println(first);

        System.out.println(last);

    }
}
```

Output:

```text
J
a
```

---

# Internal Behavior

A String behaves like an indexed sequence:

```text
J a v a
0 1 2 3
```

When you call:

```java
charAt(2)
```

Java accesses the character stored at index 2.

Result:

```text
v
```

Performance:

```
O(1)
```

Direct access.

---

# 6. Invalid Indexes

What happens here?

```java
String word = "Java";

System.out.println(word.charAt(5));
```

The String only has:

```
0 1 2 3
```

Index 5 does not exist.

Java throws:

```
StringIndexOutOfBoundsException
```

---

Safe approach:

```java
if(index < word.length()){

    System.out.println(word.charAt(index));

}
```

---

# 7. Practical Example — Inspecting a Username

Imagine a registration system:

```java
String username = "admin123";
```

We want to check:

* size
* first character
* if it is empty

Example:

```java
public class Main {

    public static void main(String[] args) {

        String username = "admin123";


        System.out.println(
            "Length: " + username.length()
        );


        System.out.println(
            "First character: " + username.charAt(0)
        );


        System.out.println(
            "Empty: " + username.isEmpty()
        );

    }
}
```

Output:

```text
Length: 8
First character: a
Empty: false
```

---

# 8. Common Mistakes

---

## Mistake 1 — Forgetting zero-based indexing

Wrong:

```java
word.charAt(1)
```

thinking it returns the first character.

Actually:

```text
Index 0 = first character
```

---

## Mistake 2 — Using length as an index

Wrong:

```java
word.charAt(word.length());
```

Example:

```text
Java

length = 4
```

Indexes:

```text
0 1 2 3
```

Index 4 does not exist.

Correct:

```java
word.charAt(word.length() - 1);
```

---

## Mistake 3 — Calling methods on null

Wrong:

```java
String name = null;

name.length();
```

Causes:

```
NullPointerException
```

Always consider whether the object exists.

---

# 9. Exercise — String Inspection Practice

Create:

```text
src/
 └── Main.java
```

Implement:

```java
String text = "Java Programming";
```

Print:

1. Total characters
2. First character
3. Last character
4. Is empty?
5. Is blank?

Expected output:

```text
Characters: 17
First: J
Last: g
Empty: false
Blank: false
```

---

# Chapter Summary

Today we learned:

✅ `length()` returns number of characters
✅ `isEmpty()` checks zero characters
✅ `isBlank()` checks empty or whitespace-only text
✅ `charAt()` accesses characters by index
✅ String indexes start at zero
✅ Invalid indexes cause exceptions
✅ String inspection methods do not modify the original String

---

# Key Mental Model

Think of a String like an array of characters:

```text
String: "Java"

Index:

0   1   2   3
J   a   v   a
```

But remember:

```text
You can read the characters.

You cannot change them.
```

---

# ✔️ Next Step

Proceed to:

# Chapter 04 — Extracting and Searching Text

Next we will learn:

* `substring()`
* `contains()`
* `startsWith()`
* `endsWith()`
* `indexOf()`
* `lastIndexOf()`

and start building real text search and extraction logic.
