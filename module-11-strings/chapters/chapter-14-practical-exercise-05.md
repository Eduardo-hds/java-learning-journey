# Chapter 14 — Practical Exercise 05: String Comparison

## Chapter Objective

In this chapter, we will build a utility that compares Strings using different approaches and explains the result of each comparison.

By the end of this chapter, you will understand:

* The difference between reference equality and content equality
* When to use `==`
* Why `equals()` is almost always the correct choice
* How `equalsIgnoreCase()` works
* How `compareTo()` performs lexicographical comparison
* How the String Pool influences comparisons
* How to present comparison results in a clear report

This chapter reinforces one of the most misunderstood topics in Java.

---

# 1. Why Compare Strings?

String comparison happens everywhere:

* Login systems
* Password validation
* Searching
* Sorting
* Filtering
* Validation
* Configuration files

Imagine:

```text
User input:
java

Stored value:
Java
```

Should they be considered equal?

Sometimes:

Yes.

Sometimes:

No.

It depends on the business rule.

---

# 2. Project Structure

We'll continue using our services.

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 │    ├── PalindromeChecker.java
 │    ├── PasswordValidator.java
 │    ├── StringAnalyzer.java
 │    ├── TextFormatter.java
 │    └── StringComparisonService.java
 └── util/
```

Responsibility:

```text
Main

↓

StringComparisonService

↓

Comparison Report
```

---

# 3. Designing the Service

Instead of placing all logic inside one method, we'll separate each comparison.

```text
StringComparisonService

├── compareReference()
├── compareContent()
├── compareIgnoringCase()
└── compareAlphabetically()
```

Each method demonstrates one concept.

---

# 4. Comparing References (`==`)

Suppose:

```java
String a = "Java";
String b = "Java";
```

Question:

```java
a == b
```

Result?

```
true
```

Why?

Because both variables reference the same object in the String Pool.

Conceptually:

```text
String Pool

┌─────────┐
│ "Java"  │
└─────────┘
   ▲   ▲
   │   │
   a   b
```

---

Now:

```java
String a = new String("Java");
String b = new String("Java");
```

Memory:

```text
Heap

┌─────────┐
│ "Java"  │
└─────────┘
    ▲
    a

┌─────────┐
│ "Java"  │
└─────────┘
    ▲
    b
```

Different objects.

Therefore:

```java
a == b
```

returns:

```
false
```

---

# 5. Implementing compareReference()

```java
public boolean compareReference(String a, String b){

    return a == b;

}
```

This method answers:

> Do both variables point to the same object?

Not:

> Do they contain the same text?

---

# 6. Comparing Content (`equals()`)

Most applications care about content.

Example:

```java
String a = new String("Java");
String b = new String("Java");
```

Even though:

```java
a == b
```

is:

```
false
```

The content is identical.

```java
a.equals(b)
```

returns:

```
true
```

---

Implementation:

```java
public boolean compareContent(String a, String b){

    return a.equals(b);

}
```

---

# 7. Comparing Ignoring Case

Sometimes capitalization doesn't matter.

Example:

```text
Java

JAVA
```

Using:

```java
equals()
```

Result:

```
false
```

Using:

```java
equalsIgnoreCase()
```

Result:

```
true
```

---

Implementation:

```java
public boolean compareIgnoringCase(String a, String b){

    return a.equalsIgnoreCase(b);

}
```

---

# 8. Alphabetical Comparison

Now let's compare ordering.

Method:

```java
compareTo()
```

This method returns an `int`.

Possible outcomes:

```text
Negative

↓

First String comes before the second.

0

↓

Strings are equal.

Positive

↓

First String comes after the second.
```

---

Example:

```java
"Apple".compareTo("Banana")
```

Result:

```
negative
```

Because:

```text
Apple

↓

comes before

↓

Banana
```

---

Example:

```java
"Banana".compareTo("Apple")
```

Result:

```
positive
```

---

Example:

```java
"Java".compareTo("Java")
```

Result:

```
0
```

---

# 9. Implementing compareAlphabetically()

```java
public int compareAlphabetically(String a, String b){

    return a.compareTo(b);

}
```

---

# 10. Interpreting compareTo()

Instead of printing:

```text
-9
```

Explain the meaning.

Example:

```java
int result =
        compareAlphabetically(a, b);

if(result == 0){

    System.out.println("Same text");

}else if(result < 0){

    System.out.println("First comes before second");

}else{

    System.out.println("First comes after second");

}
```

This makes the output much easier to understand.

---

# 11. Testing Different Cases

### Case 1

```java
String a = "Java";
String b = "Java";
```

Expected:

```text
Reference: true

Content: true

Ignore Case: true

Alphabetical: 0
```

---

### Case 2

```java
String a = new String("Java");
String b = new String("Java");
```

Expected:

```text
Reference: false

Content: true

Ignore Case: true

Alphabetical: 0
```

---

### Case 3

```java
String a = "Java";
String b = "JAVA";
```

Expected:

```text
Reference: false

Content: false

Ignore Case: true

Alphabetical:
(non-zero)
```

---

### Case 4

```java
String a = "Apple";
String b = "Banana";
```

Expected:

```text
Reference: false

Content: false

Ignore Case: false

Alphabetical:
First comes before second
```

---

# 12. Building a Comparison Report

Instead of printing isolated values:

```text
true

false

0
```

Let's build a readable report.

Example:

```text
===== String Comparison =====

First String : Java
Second String: JAVA

Reference Equal : false

Content Equal   : false

Ignore Case     : true

Alphabetical    : First comes after second

=============================
```

This is an excellent use case for:

```java
StringBuilder
```

---

# 13. Using StringBuilder

Example:

```java
StringBuilder report =
        new StringBuilder();

report.append("===== String Comparison =====\n");

report.append("Reference Equal: ")
      .append(compareReference(a,b))
      .append("\n");

report.append("Content Equal: ")
      .append(compareContent(a,b));
```

Notice that:

```java
append()
```

returns the same `StringBuilder`.

This allows:

```java
builder.append(...)
       .append(...)
       .append(...);
```

This is called **method chaining**, and it's common with mutable APIs.

---

# 14. Common Mistakes

## Mistake 1 — Using `==` for content

Wrong:

```java
if(password == "Java123")
```

Correct:

```java
if(password.equals("Java123"))
```

---

## Mistake 2 — Using `equals()` when case shouldn't matter

Login:

```text
JAVA

Java
```

If business rules ignore capitalization:

Use:

```java
equalsIgnoreCase()
```

---

## Mistake 3 — Misinterpreting compareTo()

Many beginners think:

```text
-5
```

means:

> "five positions before."

It does **not**.

Only the sign matters:

* Negative
* Zero
* Positive

Do **not** rely on the exact numeric value.

---

## Mistake 4 — Forgetting about null

This code:

```java
a.equals(b);
```

throws a `NullPointerException` if `a` is `null`.

We haven't covered null-safe comparisons yet, but it's important to remember that `equals()` assumes the object exists.

---

# Exercise Task

Create:

```text
service/
 └── StringComparisonService.java
```

Implement:

```java
compareReference()

compareContent()

compareIgnoringCase()

compareAlphabetically()
```

Then create a report using `StringBuilder`.

Test the following pairs:

### Test 1

```text
Java

Java
```

---

### Test 2

```text
Java

JAVA
```

---

### Test 3

```text
Apple

Banana
```

---

### Test 4

```java
new String("Java")

new String("Java")
```

Observe how the result of `==` changes while `equals()` does not.

---

# Chapter Summary

Today we learned:

✅ `==` compares object references
✅ `equals()` compares content
✅ `equalsIgnoreCase()` ignores capitalization
✅ `compareTo()` compares alphabetical order
✅ `StringBuilder` is useful for generating readable reports
✅ Different comparison methods solve different problems

---

# Key Mental Model

Always ask yourself:

```text
What exactly am I comparing?

Same object?

        ↓
       ==

Same text?

        ↓
    equals()

Same text ignoring case?

        ↓
equalsIgnoreCase()

Alphabetical order?

        ↓
   compareTo()
```

Choosing the correct comparison method is one of the most important habits of a Java developer.

---

# ✔️ Next Step

Proceed to:

# Chapter 15 — Practical Exercise 06: Efficient Text Construction with StringBuilder

In the next chapter, we'll build increasingly large pieces of text and compare:

* Repeated `String` concatenation
* `StringBuilder`
* Memory usage (conceptually)
* Time complexity (conceptually)

This exercise will reinforce **why `StringBuilder` exists** and prepare us for generating the reports used in the final **Text Processing Toolkit**.
