# Chapter 13 — Practical Exercise 04: Text Formatter

## Chapter Objective

In this chapter, we will build a reusable **TextFormatter** service capable of cleaning and formatting text.

By the end of this chapter, you will be able to:

* Remove unnecessary spaces
* Normalize user input
* Capitalize words
* Combine `split()`, `join()`, `substring()`, `toUpperCase()`, `toLowerCase()`, and `StringBuilder`
* Design reusable formatting methods
* Understand the trade-offs between different formatting approaches

This exercise brings together almost everything you've learned about Strings so far.

---

# 1. Why Text Formatting?

Users rarely type perfectly formatted text.

Examples:

Input:

```text
   jAvA      is    AWESOME
```

Desired output:

```text
Java Is Awesome
```

Another example:

Input:

```text
     eduardo      henrique     silva
```

Output:

```text
Eduardo Henrique Silva
```

Real applications constantly perform this kind of formatting:

* Registration forms
* Search engines
* CRMs
* Banking systems
* E-commerce
* Text editors

---

# 2. Project Structure

We'll add another service:

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 │    ├── PalindromeChecker.java
 │    ├── PasswordValidator.java
 │    ├── StringAnalyzer.java
 │    └── TextFormatter.java
 └── util/
```

Responsibility:

```text
Main
   │
   ▼
TextFormatter
   │
   ▼
Formatted text
```

---

# 3. Responsibilities of TextFormatter

Instead of one huge method:

```java
formatText()
```

We'll separate responsibilities:

```text
TextFormatter

├── removeExtraSpaces()
├── capitalizeWords()
└── normalizeText()
```

Each method performs one task.

This follows the **Single Responsibility Principle (SRP)**, which you'll revisit later when studying software design principles.

---

# 4. Removing Extra Spaces

Consider:

```text
"   Java     Programming     Bootcamp   "
```

Problems:

* Leading spaces
* Trailing spaces
* Multiple spaces between words

Desired result:

```text
Java Programming Bootcamp
```

---

## Step 1 — Remove Leading and Trailing Spaces

Use:

```java
strip()
```

Example:

```java
String text = "   Java Programming   ";

text = text.strip();
```

Result:

```text
Java Programming
```

---

## Step 2 — Remove Multiple Spaces

Conceptually:

```text
Several spaces

↓

One space
```

A practical solution is:

```java
text.split("\\s+")
```

which separates the words regardless of how many whitespace characters exist between them.

Then:

```java
String.join(" ", words);
```

rebuilds the sentence using a single space.

---

Implementation:

```java
public String removeExtraSpaces(String text){

    String clean = text.strip();

    String[] words = clean.split("\\s+");

    return String.join(" ", words);

}
```

---

# 5. Capitalizing Words

Input:

```text
java is awesome
```

Desired:

```text
Java Is Awesome
```

---

What does "capitalize" mean?

Each word should become:

```text
First letter

↓

Uppercase

Remaining letters

↓

Lowercase
```

Example:

```text
jAVA

↓

Java
```

---

# 6. Building One Capitalized Word

Suppose:

```java
String word = "jAVA";
```

We want:

First letter:

```java
word.substring(0, 1)
```

Result:

```text
j
```

Convert:

```java
.toUpperCase()
```

Result:

```text
J
```

---

Remaining letters:

```java
word.substring(1)
```

Result:

```text
AVA
```

Convert:

```java
.toLowerCase()
```

Result:

```text
ava
```

Combine:

```java
J + ava

↓

Java
```

---

# 7. Capitalizing Every Word

First:

Split the sentence.

```java
String[] words =
        text.split("\\s+");
```

Then:

Loop through each word.

Conceptually:

```text
java

↓

Java

is

↓

Is

awesome

↓

Awesome
```

---

# 8. Why Use StringBuilder Here?

If we repeatedly concatenate:

```java
result += word;
```

we create many temporary String objects.

Instead:

```java
StringBuilder builder =
        new StringBuilder();
```

allows efficient text construction.

---

# 9. Implementing capitalizeWords()

Example implementation:

```java
public String capitalizeWords(String text){

    String[] words =
            text.strip().split("\\s+");

    StringBuilder builder =
            new StringBuilder();

    for(String word : words){

        if(word.isEmpty()){
            continue;
        }

        builder.append(
                word.substring(0,1).toUpperCase()
        );

        builder.append(
                word.substring(1).toLowerCase()
        );

        builder.append(" ");

    }

    return builder.toString().strip();

}
```

---

# 10. Why Remove the Final Space?

Inside the loop we add:

```text
Word + " "
```

After the last word:

```text
Java Is Awesome_
```

(extra space)

Using:

```java
strip()
```

removes it.

Alternative solutions exist (for example, adding spaces only between words), but this one is simple and readable.

---

# 11. Creating normalizeText()

Often we want multiple formatting operations together.

Instead of calling:

```java
removeExtraSpaces()

capitalizeWords()
```

every time, we can create:

```java
public String normalizeText(String text){

    text = removeExtraSpaces(text);

    text = capitalizeWords(text);

    return text;

}
```

Now one method performs the complete normalization process.

---

# 12. Testing the Formatter

Main:

```java
import service.TextFormatter;

public class Main {

    public static void main(String[] args) {

        TextFormatter formatter =
                new TextFormatter();

        String text =
                "   jAvA     IS     awESome   ";

        System.out.println(
                formatter.normalizeText(text)
        );

    }

}
```

Output:

```text
Java Is Awesome
```

---

# 13. Another Example

Input:

```text
    eduardo      henrique      silva
```

Output:

```text
Eduardo Henrique Silva
```

---

Input:

```text
SPRING     boot
```

Output:

```text
Spring Boot
```

---

# 14. Memory Considerations

Notice what happens internally.

Original:

```text
Messy String
```

↓

`strip()`

↓

New String

↓

`split()`

↓

String[]

↓

`StringBuilder`

↓

Final String

Several temporary objects are created.

For normal applications this is perfectly acceptable.

For processing millions of texts, developers often optimize these steps to reduce object creation.

---

# 15. Performance Considerations

Current solution:

* Easy to read
* Easy to maintain
* Uses well-tested Java APIs

Performance is more than sufficient for:

* Forms
* Console applications
* Business systems

Always prefer readable code unless profiling demonstrates a real bottleneck.

---

# 16. Common Mistakes

### Mistake 1 — Forgetting lowercase conversion

Input:

```text
jAVA
```

Wrong output:

```text
JAVA
```

Correct:

```text
Java
```

---

### Mistake 2 — Ignoring multiple spaces

Input:

```text
Java      Bootcamp
```

Without normalization:

Extra spaces remain.

---

### Mistake 3 — Using String concatenation inside loops

```java
result += word;
```

For large text this creates many unnecessary String objects.

Prefer:

```java
StringBuilder
```

---

### Mistake 4 — Everything inside Main

Bad:

```text
Main

↓

Formatting logic
```

Good:

```text
Main

↓

TextFormatter

↓

Formatted result
```

---

# Exercise Task

Implement:

```text
service/
 └── TextFormatter.java
```

Create the following methods:

```java
removeExtraSpaces(String text)

capitalizeWords(String text)

normalizeText(String text)
```

Test with:

### Example 1

Input:

```text
   java     programming
```

Expected:

```text
Java Programming
```

---

### Example 2

Input:

```text
HELLO      world
```

Expected:

```text
Hello World
```

---

### Example 3

Input:

```text
      spring      BOOT      framework
```

Expected:

```text
Spring Boot Framework
```

---

# Chapter Summary

Today we learned:

✅ How to remove unnecessary spaces
✅ How to capitalize words correctly
✅ How to normalize user input
✅ How to combine multiple String APIs together
✅ Why `StringBuilder` is ideal for building formatted text
✅ How to separate formatting responsibilities into reusable methods

---

# Key Mental Model

Think of formatting as a **pipeline**:

```text
Original Text
      │
      ▼
Remove Extra Spaces
      │
      ▼
Split Into Words
      │
      ▼
Capitalize Each Word
      │
      ▼
Join Words
      │
      ▼
Formatted Text
```

Each step performs one clear transformation, making the code easier to understand and maintain.

---

# ✔️ Next Step

Proceed to:

# Chapter 14 — Practical Exercise 05: String Comparison

In the next chapter, we'll apply everything learned about:

* `==`
* `equals()`
* `equalsIgnoreCase()`
* `compareTo()`

You'll build a comparison utility that explains **why** two Strings are equal or different, reinforcing one of the most important topics in Java String handling.
