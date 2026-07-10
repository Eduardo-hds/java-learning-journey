# Chapter 15 — Practical Exercise 06: Efficient Text Construction with StringBuilder

## Chapter Objective

In this chapter, you will build increasingly larger pieces of text and understand **why `StringBuilder` exists**.

By the end of this chapter, you will be able to:

* Recognize when String concatenation becomes inefficient
* Compare `String` concatenation with `StringBuilder`
* Build large text efficiently
* Understand the memory implications of both approaches
* Use method chaining with `append()`
* Apply `StringBuilder` in real applications

This chapter focuses less on syntax (which you already know) and more on **performance and design decisions**.

---

# 1. The Problem

Suppose we want to generate a report.

Example:

```text
Student Report

Name: Eduardo
Age: 27
Course: Java Bootcamp
Status: Active
```

How should we build this text?

A beginner often writes:

```java
String report = "";

report += "Student Report\n";
report += "Name: Eduardo\n";
report += "Age: 27\n";
report += "Course: Java Bootcamp\n";
report += "Status: Active";
```

It works.

But internally, it's much more expensive than it looks.

---

# 2. What Happens Internally?

Remember:

Strings are immutable.

Every concatenation creates a new object.

Conceptually:

```text
report = ""

↓

"Student Report"

↓

"Student Report\nName: Eduardo"

↓

"Student Report\nName: Eduardo\nAge: 27"

↓

...
```

Old objects become unreachable and will eventually be removed by the Garbage Collector.

---

Suppose we concatenate 100 lines.

Conceptually:

```text
String 1

↓

String 2

↓

String 3

↓

...

↓

String 100
```

That means many temporary objects are created.

---

# 3. Using StringBuilder

Now compare:

```java
StringBuilder report = new StringBuilder();

report.append("Student Report\n");
report.append("Name: Eduardo\n");
report.append("Age: 27\n");
report.append("Course: Java Bootcamp\n");
report.append("Status: Active");
```

Internally:

```text
One object

↓

Append

↓

Append

↓

Append

↓

Append
```

The same object grows.

No unnecessary String objects are created during construction.

---

# 4. Why Is This Faster?

Imagine writing a sentence.

### String

```text
Write page

↓

Copy page

↓

Add one word

↓

Copy again

↓

Add another word
```

Lots of copying.

---

### StringBuilder

```text
Notebook

↓

Write next word

↓

Write next word

↓

Write next word
```

Same notebook.

Much less work.

---

# 5. Method Chaining

Because `append()` returns the same object:

```java
builder.append("Java")
       .append(" ")
       .append("Bootcamp")
       .append(" ")
       .append("2026");
```

This is equivalent to:

```java
builder.append("Java");
builder.append(" ");
builder.append("Bootcamp");
builder.append(" ");
builder.append("2026");
```

Choose the style that your team finds most readable.

---

# 6. Creating a Report

Let's create a reusable service.

Project structure:

```text
src/
 ├── Main.java
 ├── model/
 │    └── User.java
 ├── service/
 │    ├── ReportBuilder.java
 │    ├── TextFormatter.java
 │    ├── StringAnalyzer.java
 │    └── PasswordValidator.java
 └── util/
```

---

# 7. The User Model

Create:

```text
model/
 └── User.java
```

Example:

```java
package model;

public class User {

    private String name;
    private int age;
    private String role;

    // Constructor

    // Getters

}
```

Notice:

The model stores data.

It does **not** build reports.

---

# 8. Creating ReportBuilder

```text
service/
 └── ReportBuilder.java
```

Responsibility:

```text
Receive User

↓

Generate formatted report

↓

Return String
```

---

Method:

```java
public String buildReport(User user){

}
```

---

# 9. Building the Report

Inside the method:

```java
StringBuilder report = new StringBuilder();

report.append("===== USER REPORT =====\n");

report.append("Name: ")
      .append(user.getName())
      .append("\n");

report.append("Age: ")
      .append(user.getAge())
      .append("\n");

report.append("Role: ")
      .append(user.getRole())
      .append("\n");

report.append("======================");

return report.toString();
```

---

Output:

```text
===== USER REPORT =====

Name: Eduardo
Age: 27
Role: Java Student

======================
```

---

# 10. Why Return String Instead of StringBuilder?

Your service is generating **text**.

The caller usually wants:

```java
System.out.println(report);
```

or

```java
save(report);
```

Both expect a `String`.

Returning:

```java
String
```

hides the implementation details.

This is a good example of **encapsulation**.

If one day you decide to stop using `StringBuilder`, callers won't need to change.

---

# 11. Memory Comparison

### String Concatenation

Conceptually:

```text
Object 1

↓

Object 2

↓

Object 3

↓

Object 4

↓

Final Object
```

Many temporary allocations.

---

### StringBuilder

```text
One Object

↓

Expanded

↓

Expanded

↓

Expanded

↓

Finished
```

Much less garbage.

---

# 12. Time Complexity (Conceptual)

Suppose we build a text with 10,000 lines.

### String

Each concatenation copies all previous characters.

The amount of work grows rapidly.

Conceptually:

```text
1

↓

2

↓

3

↓

...

↓

10,000
```

Repeated copying.

---

### StringBuilder

Each append simply adds new characters.

Much closer to linear growth.

---

We won't measure execution time here, but this difference becomes very noticeable with large amounts of text.

---

# 13. Real-World Use Cases

`StringBuilder` is commonly used for:

* Building reports
* Generating SQL queries
* Producing JSON manually
* Creating CSV content
* Generating HTML
* Building logs
* Producing console output

Whenever you're **gradually constructing text**, think about `StringBuilder`.

---

# 14. When NOT to Use StringBuilder

Suppose:

```java
String language = "Java";
```

Done.

No modification.

Using:

```java
StringBuilder builder =
        new StringBuilder("Java");
```

adds unnecessary complexity.

Rule of thumb:

* Fixed text → `String`
* Growing text → `StringBuilder`

---

# 15. Common Mistakes

### Mistake 1 — Returning StringBuilder

Avoid exposing implementation details.

Prefer:

```java
public String buildReport(...)
```

instead of:

```java
public StringBuilder buildReport(...)
```

---

### Mistake 2 — Creating Many Builders

Bad:

```java
StringBuilder a = new StringBuilder();
StringBuilder b = new StringBuilder();
StringBuilder c = new StringBuilder();
```

when one builder is enough.

---

### Mistake 3 — Using String Concatenation Inside Loops

```java
for (...) {

    result += value;

}
```

Prefer:

```java
for (...) {

    builder.append(value);

}
```

---

### Mistake 4 — Forgetting `toString()`

A `StringBuilder` is **not** a `String`.

Convert it when you're finished.

---

# Exercise Task

Create:

```text
model/
 └── User.java
```

and

```text
service/
 └── ReportBuilder.java
```

Requirements:

Implement:

```java
public String buildReport(User user)
```

The report must include:

* Name
* Age
* Role

Use only:

* `StringBuilder`
* `append()`
* `toString()`

Do **not** use repeated String concatenation.

---

# Challenge

Modify the report to include:

```text
===== USER REPORT =====

Name:
Age:
Role:

Summary:
<Generate one sentence describing the user>

======================
```

Build the summary using additional `append()` calls.

---

# Chapter Summary

Today we learned:

✅ Why repeated String concatenation is inefficient
✅ How `StringBuilder` avoids unnecessary object creation
✅ How method chaining improves readability
✅ Why services should return `String` instead of `StringBuilder`
✅ How to organize report generation into dedicated classes
✅ When `StringBuilder` should and should not be used

---

# Key Mental Model

Whenever you're creating text **piece by piece**, think:

```text
Need to build text gradually?

        │
        ▼
Use StringBuilder

Need fixed text?

        │
        ▼
Use String
```

Choosing the right tool is not just about performance—it also makes your intent clear to anyone reading your code.

---

# ✔️ Next Step

Proceed to:

# Chapter 16 — Practical Exercise 07: Text Statistics (Final Exercise Before the Project)

In the final exercise of this module, you'll combine everything you've learned to generate a complete **Text Statistics Report**, including:

* Total characters
* Total words
* Total vowels
* Total consonants
* Average word length
* Longest word
* Shortest word

This exercise will directly prepare the core functionality of the **Text Processing Toolkit** final project.
