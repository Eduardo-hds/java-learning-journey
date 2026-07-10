# Chapter 06 — Comparing Strings Correctly

## Chapter Objective

By the end of this chapter, you should understand:

* The difference between reference comparison and content comparison
* Why `==` is usually wrong for Strings
* How `equals()` works internally
* When to use `equalsIgnoreCase()`
* How `compareTo()` works
* How String comparison is used in real applications
* Common mistakes when comparing text

---

# 1. Why String Comparison Is Confusing

One of the most common mistakes in Java is:

```java
String a = "Java";

if(a == "Java"){
    
}
```

Many beginners think:

> "The text is Java, so this should work."

Sometimes it works.

Sometimes it does not.

Why?

Because Strings are objects.

When comparing objects, Java has two different questions:

---

## Question 1

> Are these the exact same object in memory?

This is:

```java
==
```

---

## Question 2

> Do these objects contain the same text?

This is:

```java
equals()
```

These are completely different comparisons.

---

# 2. The `==` Operator

## What does `==` do?

For objects:

```java
==
```

compares references.

It asks:

> Do both variables point to the same object?

---

Example:

```java
String a = "Java";

String b = "Java";

System.out.println(a == b);
```

Output:

```text
true
```

Why?

Because both use the String Pool.

Memory:

```text
String Pool

+---------+
| Java    |
+---------+
    ^
    |
  a,b
```

Both references point to the same object.

---

# 3. Why `==` Can Fail

Now:

```java
String a = new String("Java");

String b = new String("Java");

System.out.println(a == b);
```

Output:

```text
false
```

Why?

Because:

```text
Heap

+---------+
| Java    |
+---------+
    ^
    |
    a


+---------+
| Java    |
+---------+
    ^
    |
    b
```

Two different objects.

The content is equal.

The references are different.

---

# 4. The Golden Rule

For Strings:

## Never use:

```java
==
```

to compare content.

Use:

```java
equals()
```

---

# 5. The `equals()` Method

## What is it?

`equals()` compares the actual content of Strings.

Example:

```java
String a = new String("Java");

String b = new String("Java");

System.out.println(
    a.equals(b)
);
```

Output:

```text
true
```

Because:

```text
Java
=
Java
```

---

# Internal Behavior

Conceptually:

```text
a
 |
 v
"Java"


b
 |
 v
"Java"
```

`equals()` checks:

Character by character:

```text
J == J
a == a
v == v
a == a
```

Everything matches.

Result:

```text
true
```

---

# 6. How `equals()` Works With Null

Example:

```java
String name = null;

name.equals("Java");
```

Problem:

There is no object.

Result:

```text
NullPointerException
```

---

Safer approach:

```java
"Java".equals(name);
```

Now:

* `"Java"` exists
* comparison is safe

Example:

```java
String input = null;

if("admin".equals(input)){

    System.out.println("Valid");

}
```

No crash.

---

# 7. The `equalsIgnoreCase()` Method

## What is it?

Compares Strings ignoring uppercase/lowercase differences.

Example:

```java
String a = "java";

String b = "JAVA";

System.out.println(
    a.equalsIgnoreCase(b)
);
```

Output:

```text
true
```

---

Without it:

```java
a.equals(b);
```

Result:

```text
false
```

Because:

```text
java

!=

JAVA
```

---

# Real-world Uses

Very common in:

* usernames
* commands
* categories
* user input

Example:

```java
String command = "EXIT";

if(command.equalsIgnoreCase("exit")){

    System.out.println("Closing program");

}
```

Works with:

```text
exit
EXIT
Exit
eXiT
```

---

# 8. `equals()` vs `equalsIgnoreCase()`

Comparison:

| Method               | Case Sensitive? |
| -------------------- | --------------- |
| `equals()`           | Yes             |
| `equalsIgnoreCase()` | No              |

Example:

```java
"Java".equals("java")
```

Result:

```text
false
```

---

```java
"Java".equalsIgnoreCase("java")
```

Result:

```text
true
```

---

# 9. The `compareTo()` Method

## What is it?

`compareTo()` compares Strings alphabetically.

It returns:

* negative number
* zero
* positive number

---

Example:

```java
String a = "Apple";

String b = "Banana";

System.out.println(
    a.compareTo(b)
);
```

Output:

```text
negative value
```

Why?

Because:

```text
Apple

comes before

Banana
```

---

# 10. Understanding the Result

## Case 1 — Equal

```java
"Java".compareTo("Java")
```

Result:

```text
0
```

Meaning:

```text
Both are equal
```

---

## Case 2 — First comes before second

```java
"Apple".compareTo("Banana")
```

Result:

```text
negative
```

Meaning:

```text
Apple < Banana
```

---

## Case 3 — First comes after second

```java
"Zoo".compareTo("Apple")
```

Result:

```text
positive
```

Meaning:

```text
Zoo > Apple
```

---

# 11. How Does `compareTo()` Work Internally?

It compares Unicode values.

Example:

```text
A = 65

B = 66
```

Therefore:

```text
A < B
```

---

Example:

```java
"Apple".compareTo("Banana")
```

Comparison:

```text
A vs B
```

Since:

```text
A < B
```

Result:

```text
negative
```

---

# 12. Using `compareTo()` for Sorting

Example:

```java
String[] names = {
    "Carlos",
    "Ana",
    "Bruno"
};
```

Sorting requires knowing:

```text
Who comes first?
```

`compareTo()` provides this information.

Example:

```java
System.out.println(
    "Ana".compareTo("Bruno")
);
```

Result:

```text
negative
```

Meaning:

```text
Ana comes before Bruno
```

---

# 13. Comparison Examples

Let's analyze:

```java
String a = "Java";

String b = "java";

String c = new String("Java");
```

---

## Example 1

```java
a == b
```

Result:

```text
false
```

Different objects/content.

---

## Example 2

```java
a.equals(b)
```

Result:

```text
false
```

Case difference.

---

## Example 3

```java
a.equalsIgnoreCase(b)
```

Result:

```text
true
```

Case ignored.

---

## Example 4

```java
a.equals(c)
```

Result:

```text
true
```

Same content.

---

## Example 5

```java
a == c
```

Result:

```text
false
```

Different objects.

---

# 14. Practical Example — Login System

Imagine:

```java
String storedUsername = "admin";

String inputUsername = "ADMIN";
```

Using:

```java
==
```

Wrong:

```java
if(storedUsername == inputUsername)
```

May fail.

---

Using:

```java
equalsIgnoreCase()
```

Correct:

```java
if(storedUsername.equalsIgnoreCase(inputUsername)){

    System.out.println("Login accepted");

}
```

---

# 15. Common Mistakes

---

## Mistake 1 — Using `==`

Wrong:

```java
if(password == "1234")
```

Correct:

```java
if(password.equals("1234"))
```

---

## Mistake 2 — Calling equals on possible null values

Dangerous:

```java
input.equals("yes");
```

Safer:

```java
"yes".equals(input);
```

---

## Mistake 3 — Forgetting case sensitivity

Example:

```java
"JAVA".equals("java")
```

Result:

```text
false
```

Use:

```java
equalsIgnoreCase()
```

when appropriate.

---

# 16. Practice Exercise — String Comparison Lab

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

        String second = "JAVA";

        String third = new String("Java");


        System.out.println(first == second);

        System.out.println(first == third);

        System.out.println(first.equals(second));

        System.out.println(first.equalsIgnoreCase(second));

        System.out.println(first.equals(third));

        System.out.println(first.compareTo(second));

    }
}
```

Analyze each result.

Expected concepts:

```text
==          -> reference
equals      -> content
ignoreCase  -> content without case
compareTo   -> ordering
```

---

# Chapter Summary

Today we learned:

✅ `==` compares references
✅ `equals()` compares content
✅ `equalsIgnoreCase()` ignores capitalization
✅ `compareTo()` compares alphabetical order
✅ String Pool explains why `==` sometimes appears to work
✅ Content comparison should use `equals()`
✅ Null safety matters when comparing Strings

---

# Key Mental Model

Remember:

```text
==

"Are these the same object?"


equals()

"Do these objects contain the same text?"
```

For Strings:

```text
Use equals()
```

not:

```text
==
```

---

# ✔️ Next Step

Proceed to:

# Chapter 07 — Splitting and Joining Text

Next we will learn:

* `split()`
* `join()`

and how to break text into pieces and rebuild text efficiently.
