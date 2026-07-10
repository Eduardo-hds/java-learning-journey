# Chapter 04 — Extracting and Searching Text

## Chapter Objective

By the end of this chapter, you should understand:

* How to extract parts of a String
* How to search for text inside another String
* How Java handles indexes during extraction
* The difference between finding text and checking existence
* How these methods are used in real applications
* Common mistakes when working with indexes

---

# 1. Working With Portions of Text

In real applications, we rarely work with complete text only.

Examples:

* Extracting a username from an email
* Getting a file extension
* Searching messages
* Validating prefixes
* Processing commands

Example:

```java
String email = "user@gmail.com";
```

We may want:

```text
user
```

or:

```text
gmail.com
```

Java provides methods for this.

---

# 2. The `substring()` Method

## What is it?

`substring()` extracts a portion of a String.

Important:

It does **not modify** the original String.

Because Strings are immutable.

---

There are two versions:

```java
substring(beginIndex)
```

and:

```java
substring(beginIndex, endIndex)
```

---

# 3. `substring(beginIndex)`

## Syntax

```java
String result = text.substring(start);
```

It returns everything from `start` until the end.

---

Example:

```java
String language = "Programming";

String part = language.substring(7);

System.out.println(part);
```

Let's map indexes:

```text
P r o g r a m m i n g

0 1 2 3 4 5 6 7 8 9 10
```

Starting at:

```text
index 7
```

we get:

```text
m i n g
```

Output:

```text
ming
```

---

# 4. `substring(beginIndex, endIndex)`

## Syntax

```java
String result = text.substring(start, end);
```

Important rule:

> The beginning index is included. The ending index is excluded.

Example:

```java
String word = "Java";

String part = word.substring(0, 2);

System.out.println(part);
```

Indexes:

```text
J a v a

0 1 2 3
```

Range:

```text
0 -------- 2
```

Includes:

```text
J a
```

Does not include:

```text
v
```

Output:

```text
Ja
```

---

# Why is the end excluded?

This design makes calculations easier.

Example:

```java
substring(0, text.length())
```

returns the entire String.

Also:

```java
substring(0, 4)
```

means:

```text
characters from position 0 up to 4
```

which has size:

```text
4 - 0 = 4 characters
```

---

# 5. Common `substring()` Mistakes

## Mistake 1 — Forgetting zero-based indexes

Wrong thinking:

```text
First character = index 1
```

Correct:

```text
First character = index 0
```

---

## Mistake 2 — Including the end index

Example:

```java
String text = "Java";

text.substring(0,3);
```

Some expect:

```text
Java
```

but result:

```text
Jav
```

Because index 3 is excluded.

---

## Mistake 3 — Invalid range

Example:

```java
String text = "Java";

text.substring(5);
```

There is no index 5.

Result:

```text
StringIndexOutOfBoundsException
```

---

# Practical Example — Extract Username From Email

Input:

```java
String email = "eduardo@gmail.com";
```

We want:

```text
eduardo
```

Algorithm:

1. Find `@`
2. Extract everything before it

Example:

```java
public class Main {

    public static void main(String[] args) {

        String email = "eduardo@gmail.com";

        int position = email.indexOf("@");

        String username = email.substring(0, position);

        System.out.println(username);

    }
}
```

Output:

```text
eduardo
```

We combined:

```text
indexOf()
substring()
```

This is a very common pattern.

---

# 6. The `contains()` Method

## What is it?

Checks whether a String contains another String.

Returns:

```java
true
```

or:

```java
false
```

---

Example:

```java
String message = "Welcome to Java";

System.out.println(
    message.contains("Java")
);
```

Output:

```text
true
```

---

Another example:

```java
message.contains("Python");
```

Output:

```text
false
```

---

# Internally

Conceptually:

```text
"Welcome to Java"

Search:

"Java"
```

Java checks if the sequence exists.

---

# When to Use

Good for:

* searching keywords
* validation
* filtering text

Example:

```java
if(message.contains("error")){

    System.out.println("Problem detected");

}
```

---

# Case Sensitivity

Important:

```java
String text = "Java";
```

This:

```java
text.contains("java");
```

returns:

```text
false
```

because:

```text
Java
java
```

are different.

Later we will combine this with:

```java
toLowerCase()
```

for case-insensitive searches.

---

# 7. The `startsWith()` Method

## What is it?

Checks whether a String begins with a specific sequence.

Example:

```java
String file = "report.pdf";

System.out.println(
    file.startsWith("report")
);
```

Output:

```text
true
```

---

Another example:

```java
file.startsWith("image");
```

Output:

```text
false
```

---

# Real-world Uses

Examples:

Checking:

```text
https://
```

in URLs:

```java
if(url.startsWith("https")){

}
```

Checking commands:

```text
/help
```

---

# 8. The `endsWith()` Method

## What is it?

Checks whether a String ends with a specific sequence.

Example:

```java
String file = "photo.png";

System.out.println(
    file.endsWith(".png")
);
```

Output:

```text
true
```

---

Common uses:

File types:

```text
.jpg
.png
.txt
```

Validation:

```java
if(email.endsWith("@company.com")){

}
```

---

# 9. The `indexOf()` Method

## What is it?

Finds the position of the first occurrence of text.

Returns:

* index position
* `-1` if not found

---

Example:

```java
String text = "Java Programming";

System.out.println(
    text.indexOf("a")
);
```

Output:

```text
1
```

Because:

```text
J a v a

0 1 2 3
```

---

If not found:

```java
text.indexOf("Python");
```

Output:

```text
-1
```

---

# Why return -1?

Because valid indexes start at:

```text
0
```

So:

```text
-1
```

means:

> There is no valid position.

---

# Example

```java
String message = "Hello World";

int position = message.indexOf("World");

System.out.println(position);
```

Output:

```text
6
```

---

# 10. The `lastIndexOf()` Method

## What is it?

Finds the last occurrence of text.

Example:

```java
String text = "banana";

System.out.println(
    text.lastIndexOf("a")
);
```

Indexes:

```text
b a n a n a

0 1 2 3 4 5
```

There are three `a` characters:

```text
1
3
5
```

The last one:

```text
5
```

Output:

```text
5
```

---

# Practical Example — Finding File Extension

Input:

```java
String file = "photo.profile.png";
```

We want:

```text
png
```

The last dot matters.

Code:

```java
public class Main {

    public static void main(String[] args) {

        String file = "photo.profile.png";

        int dot = file.lastIndexOf(".");

        String extension = file.substring(dot + 1);

        System.out.println(extension);

    }
}
```

Output:

```text
png
```

---

# 11. Combining Search Methods

Real applications combine these methods.

Example:

Validate an email:

```java
String email = "user@gmail.com";
```

Check:

```java
contains("@")
```

Extract:

```java
substring()
```

Find:

```java
indexOf()
```

---

# Complete Example

```java
public class Main {

    public static void main(String[] args) {

        String email = "admin@example.com";


        if(email.contains("@")){

            int position = email.indexOf("@");

            String user = email.substring(0, position);

            String domain = email.substring(position + 1);


            System.out.println("User: " + user);

            System.out.println("Domain: " + domain);

        }

    }
}
```

Output:

```text
User: admin
Domain: example.com
```

---

# 12. Performance Considerations

Most searching operations:

```java
contains()
indexOf()
lastIndexOf()
```

need to inspect characters.

For small Strings:

```text
"Java"
```

the difference is irrelevant.

For very large texts:

```text
millions of characters
```

the choice of algorithm matters.

For this module:

Focus on:

* correct usage
* avoiding unnecessary processing

---

# Chapter Summary

Today we learned:

✅ `substring()` extracts parts of Strings
✅ The end index is exclusive
✅ `contains()` searches for text existence
✅ `startsWith()` checks beginnings
✅ `endsWith()` checks endings
✅ `indexOf()` finds the first occurrence
✅ `lastIndexOf()` finds the last occurrence
✅ Search methods return `-1` when nothing is found
✅ Combining methods allows powerful text processing

---

# Key Mental Model

Think of Strings as indexed text:

```text
Java Programming

0123456789...
```

Searching finds positions:

```text
indexOf()
      |
      v
position
```

Extracting uses positions:

```text
substring()
      |
      v
new String
```

---

# Practice Exercise

Create a program that receives:

```java
String sentence = "Java is a powerful programming language";
```

Your program should print:

1. Whether it contains `"Java"`
2. The position of `"programming"`
3. The first 4 characters
4. The last 8 characters
5. Whether it starts with `"Java"`
6. Whether it ends with `"language"`

Expected:

```text
Contains Java: true
Programming position: 16
First 4: Java
Last 8: language
Starts with Java: true
Ends with language: true
```

---

# ✔️ Next Step

Proceed to:

# Chapter 05 — Transforming Strings

Next we will learn how to create modified versions of text using:

* `replace()`
* `replaceFirst()`
* `toUpperCase()`
* `toLowerCase()`
* `trim()`
* `strip()`
* `repeat()`

and understand why every transformation creates a new String object.
