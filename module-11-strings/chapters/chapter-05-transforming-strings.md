# Chapter 05 — Transforming Strings

## Chapter Objective

By the end of this chapter, you should understand:

* How to transform String content
* Why String transformations create new objects
* The difference between replacing and modifying
* How to normalize text
* How to remove unnecessary spaces
* When transformations can impact performance
* Common mistakes when working with immutable Strings

---

# 1. String Transformation and Immutability

Before learning transformation methods, remember:

> A String cannot be modified after creation.

This means:

```java
String text = "java";
```

is permanently:

```text
java
```

If we transform it:

```java
text.toUpperCase();
```

Java does not change:

```text
java
```

Instead, it creates:

```text
JAVA
```

as a new String object.

---

Example:

```java
public class Main {

    public static void main(String[] args) {

        String text = "java";

        text.toUpperCase();

        System.out.println(text);

    }
}
```

Output:

```text
java
```

---

Correct:

```java
text = text.toUpperCase();
```

Now:

```text
JAVA
```

---

# 2. The `replace()` Method

## What is it?

`replace()` creates a new String replacing all occurrences of a character or sequence.

Syntax:

```java
replace(oldValue, newValue)
```

---

Example:

```java
String text = "Java";

String result = text.replace("a", "o");

System.out.println(result);
```

Output:

```text
Jovo
```

---

Original:

```text
Java
```

remains unchanged.

```java
System.out.println(text);
```

Output:

```text
Java
```

---

# Internal Behavior

Before:

```text
text
 |
 v
"Java"
```

After:

```text
text
 |
 v
"Java"


result
 |
 v
"Jovo"
```

Two different objects.

---

# Replacing Characters

Example:

```java
String phone = "123-456-789";

String clean = phone.replace("-", "");

System.out.println(clean);
```

Output:

```text
123456789
```

Common use:

* removing formatting
* cleaning user input

---

# Replacing Words

Example:

```java
String message = "I like Python";

message = message.replace(
    "Python",
    "Java"
);

System.out.println(message);
```

Output:

```text
I like Java
```

---

# When to Use `replace()`

Good for:

* replacing all occurrences
* text cleaning
* normalization

Examples:

```text
Remove:
"-"
"_"
" "

Replace:
old words
symbols
characters
```

---

# 3. The `replaceFirst()` Method

## What is it?

`replaceFirst()` replaces only the first occurrence.

Example:

```java
String text = "cat cat cat";

String result = text.replaceFirst(
    "cat",
    "dog"
);

System.out.println(result);
```

Output:

```text
dog cat cat
```

---

Compare:

## replace()

```java
text.replace("cat", "dog");
```

Result:

```text
dog dog dog
```

---

## replaceFirst()

```java
text.replaceFirst("cat", "dog");
```

Result:

```text
dog cat cat
```

---

# Important Note

`replaceFirst()` internally works with regular expressions.

For this module, understand only the basic behavior:

> Replace the first matching occurrence.

Regex itself will be studied later.

---

# 4. The `toUpperCase()` Method

## What is it?

Converts characters to uppercase.

Example:

```java
String name = "java";

String result = name.toUpperCase();

System.out.println(result);
```

Output:

```text
JAVA
```

---

Original:

```text
java
```

is unchanged.

---

# Real-world Uses

Examples:

## Case normalization

Input:

```text
Java
JAVA
java
```

Convert all to:

```text
JAVA
```

Then comparisons become easier.

---

Example:

```java
String language = "Java";

if(language.toUpperCase().equals("JAVA")){

    System.out.println("Matched");

}
```

---

# 5. The `toLowerCase()` Method

Opposite operation.

Example:

```java
String text = "JAVA";

System.out.println(
    text.toLowerCase()
);
```

Output:

```text
java
```

---

# Common Pattern

Case-insensitive search:

```java
String message = "ERROR: File missing";

if(message.toLowerCase().contains("error")){

    System.out.println("Error found");

}
```

Output:

```text
Error found
```

---

# Performance Consideration

Avoid unnecessary transformations.

Example:

```java
if(text.toLowerCase().contains("java"))
```

creates a new String every time.

For small text:

No problem.

For large processing:

Be careful.

---

# 6. The `trim()` Method

## What is it?

Removes whitespace from the beginning and end of a String.

Example:

```java
String text = "   Java   ";

String result = text.trim();

System.out.println(result);
```

Output:

```text
Java
```

---

Important:

It removes:

```text
before text
after text
```

but not:

```text
inside text
```

Example:

```java
String text = "Java   Programming";

System.out.println(text.trim());
```

Output:

```text
Java   Programming
```

The middle spaces remain.

---

# Common Use Case

User input:

```java
String username = "   admin   ";
```

Without cleaning:

```text
"   admin   "
```

With:

```java
username.trim()
```

Result:

```text
"admin"
```

---

# 7. The `strip()` Method

## What is it?

`strip()` is a newer alternative introduced in Java 11.

It also removes whitespace from the beginning and end.

Example:

```java
String text = "   Java   ";

System.out.println(
    text.strip()
);
```

Output:

```text
Java
```

---

# trim() vs strip()

The difference:

## trim()

Uses older ASCII-based rules.

## strip()

Uses Unicode-aware whitespace detection.

Example:

Some characters from other languages are considered whitespace by Unicode.

`strip()` handles them better.

---

Modern Java:

Prefer:

```java
strip()
```

when you want proper Unicode support.

---

# 8. The `repeat()` Method

## What is it?

Creates a String repeated multiple times.

Example:

```java
String line = "-";

System.out.println(
    line.repeat(10)
);
```

Output:

```text
----------
```

---

Another example:

```java
String word = "Java ";

System.out.println(
    word.repeat(3)
);
```

Output:

```text
Java Java Java 
```

---

# Common Uses

Formatting:

```java
System.out.println(
    "=".repeat(30)
);
```

Output:

```text
==============================
```

Creating separators:

```text
----------------------
```

---

# 9. Combining Transformations

Real applications combine methods.

Example:

Normalize a username:

Input:

```text
"   Eduardo   "
```

Process:

```java
String username =
    input
    .strip()
    .toLowerCase();
```

Result:

```text
eduardo
```

---

Example:

```java
public class Main {

    public static void main(String[] args) {

        String username = "   EDUARDO   ";

        username = username
                .strip()
                .toLowerCase();

        System.out.println(username);

    }
}
```

Output:

```text
eduardo
```

---

# 10. Chaining Methods

Java allows method chaining:

```java
text
    .strip()
    .toLowerCase()
    .replace("java", "python");
```

Execution order:

1. `strip()`
2. `toLowerCase()`
3. `replace()`

Each returns a new String.

---

Conceptually:

```text
Original

"   JAVA   "


strip()

"JAVA"


toLowerCase()

"java"


replace()

"python"
```

---

# 11. Memory Impact

Consider:

```java
String text = "Java";

text
    .toUpperCase()
    .replace("JAVA", "PYTHON");
```

Objects created:

```text
"Java"

"JAVA"

"PYTHON"
```

The original remains.

---

For normal usage:

Fine.

For huge loops:

Problematic.

Example:

```java
for(int i = 0; i < 100000; i++){

    text = text.toUpperCase();

}
```

Creates many temporary objects.

---

Later:

```java
StringBuilder
```

will solve many repeated modification problems.

---

# 12. Practice Exercise — Text Normalizer

Create:

```text
src/
 └── Main.java
```

Given:

```java
String text = "   JAVA programming LANGUAGE   ";
```

Transform it into:

```text
Java programming language
```

Requirements:

1. Remove extra spaces at beginning and end
2. Convert to lowercase
3. Replace `"java"` with `"Java"`

Expected:

```text
Java programming language
```

---

# Chapter Summary

Today we learned:

✅ Strings cannot be modified directly
✅ Transformation methods create new Strings
✅ `replace()` changes all occurrences
✅ `replaceFirst()` changes only the first occurrence
✅ `toUpperCase()` converts text to uppercase
✅ `toLowerCase()` converts text to lowercase
✅ `trim()` removes simple surrounding spaces
✅ `strip()` handles Unicode whitespace better
✅ `repeat()` duplicates text
✅ Method chaining creates transformation pipelines

---

# Key Mental Model

Remember:

```text
String transformation:

Original String
        |
        v
New String
```

Methods do not edit the existing object.

They create a new version.

---

# ✔️ Next Step

Proceed to:

# Chapter 06 — Comparing Strings Correctly

Next we will learn:

* `==`
* `equals()`
* `equalsIgnoreCase()`
* `compareTo()`

and understand the most common String mistake in Java:

> Why `==` compares objects, not text.
