# Chapter 8 — `throw`

So far, every exception we've seen has been thrown **automatically by Java**.

Examples:

* Dividing by zero throws an `ArithmeticException`.
* Parsing invalid text throws a `NumberFormatException`.
* Accessing a null reference throws a `NullPointerException`.

But what if **your own business rules** detect an invalid situation?

For example:

* A student's age cannot be negative.
* A bank account cannot have a negative deposit.
* A withdrawal cannot exceed the account balance.
* A username cannot be empty.

Java cannot know these business rules.

It is **your responsibility** to detect these situations and throw an exception when necessary.

This is the purpose of the `throw` keyword.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What `throw` does
* The difference between `throw` and `throws`
* How to throw exceptions manually
* How to validate business rules
* Guard clauses
* When to throw exceptions
* When not to throw exceptions
* Best practices used in professional applications

---

# Automatic vs Manual Exceptions

Until now, Java has thrown exceptions for us.

Example:

```java
int result = 10 / 0;
```

Java detects the invalid operation and automatically throws:

```java
ArithmeticException
```

Now consider this method:

```java
public void setAge(int age) {

}
```

Should Java know whether an age of `-10` is valid?

No.

Only your application knows the business rules.

If the rule says age must be positive, **you** must throw the exception.

---

# What is `throw`?

The `throw` keyword creates (or reuses) an exception object and immediately interrupts the normal execution flow.

Basic syntax:

```java
throw new ExceptionType("Message");
```

Example:

```java
throw new IllegalArgumentException("Age cannot be negative.");
```

Once this line executes:

* The exception is thrown.
* The current method stops executing immediately.
* Java begins searching for a matching `catch`.
* If no handler is found, the exception propagates.

---

# First Example

```java
public class Main {

    public static void main(String[] args) {

        throw new IllegalArgumentException("Invalid value.");

    }

}
```

Output:

```text
Exception in thread "main"
java.lang.IllegalArgumentException: Invalid value.
```

Even though we created the exception ourselves, Java treats it exactly like any built-in exception.

---

# Execution Stops Immediately

Consider this example:

```java
System.out.println("Start");

throw new IllegalArgumentException("Invalid input.");

System.out.println("End");
```

Output:

```text
Start

Exception in thread "main"
java.lang.IllegalArgumentException: Invalid input.
```

The last line is never executed.

Throwing an exception immediately interrupts the current execution flow.

---

# Using `throw` Inside an `if`

Most manual exceptions are thrown after validating data.

Example:

```java
public void setAge(int age) {

    if (age < 0) {

        throw new IllegalArgumentException("Age cannot be negative.");

    }

    System.out.println("Age accepted.");

}
```

This pattern is extremely common in professional software.

---

# Guard Clauses

A **guard clause** is an early validation that immediately rejects invalid input.

Example:

```java
public void withdraw(double amount) {

    if (amount <= 0) {

        throw new IllegalArgumentException(
            "Withdrawal amount must be greater than zero."
        );

    }

    System.out.println("Processing withdrawal...");

}
```

Instead of allowing invalid data to continue through the method, the method fails immediately.

This is known as **fail-fast programming**.

---

# Why Fail Fast?

Imagine this method:

```java
public void createStudent(int age) {

    // dozens of lines

    // more processing

    // even more processing

}
```

If the age is invalid, should the method perform all that work first?

No.

Validate immediately.

Example:

```java
public void createStudent(int age) {

    if (age < 0) {

        throw new IllegalArgumentException(
            "Age cannot be negative."
        );

    }

    // remaining code

}
```

This makes bugs easier to detect and prevents invalid data from spreading through the application.

---

# Throwing Different Exceptions

You are not limited to `IllegalArgumentException`.

Examples:

```java
throw new ArithmeticException("Invalid calculation.");
```

```java
throw new RuntimeException("Unexpected error.");
```

```java
throw new NullPointerException("Student cannot be null.");
```

Later in this module, we'll create our own custom exceptions such as:

```java
throw new InvalidAgeException("Age must be at least 18.");
```

These provide much clearer information than generic exceptions.

---

# Using `throw` with `try/catch`

An exception you throw yourself can be handled just like one thrown by Java.

Example:

```java
public class Main {

    public static void main(String[] args) {

        try {

            validateAge(-5);

        } catch (IllegalArgumentException e) {

            System.out.println(e.getMessage());

        }

    }

    static void validateAge(int age) {

        if (age < 0) {

            throw new IllegalArgumentException(
                "Age cannot be negative."
            );

        }

    }

}
```

Output:

```text
Age cannot be negative.
```

---

# `throw` vs `throws`

These two keywords are often confused.

They serve completely different purposes.

| `throw`                          | `throws`                                      |
| -------------------------------- | --------------------------------------------- |
| Actually throws an exception     | Declares that a method may throw an exception |
| Used inside a method             | Used in the method declaration                |
| Interrupts execution immediately | Does not throw anything by itself             |

Example:

```java
throw new IllegalArgumentException("Invalid age.");
```

versus

```java
public void save() throws IOException {

}
```

We'll study `throws` in detail in the next chapter.

---

# When Should You Throw an Exception?

Throw an exception when:

* A business rule is violated.
* A method receives invalid arguments.
* Continuing execution would leave the application in an invalid state.
* A required object is missing.
* An impossible situation has occurred.

---

# When Should You NOT Throw an Exception?

Not every invalid condition should become an exception.

Suppose you are checking whether a menu option exists.

```java
if (option == 1) {

    // execute option

}
```

There is no need to throw an exception here if the user can simply choose another option.

Exceptions are for **exceptional situations**, not ordinary control flow.

---

# Choosing the Right Exception

For invalid method arguments, Java already provides:

```java
IllegalArgumentException
```

For invalid object state:

```java
IllegalStateException
```

For null values:

```java
NullPointerException
```

When none of the built-in exceptions clearly describes your business rule, create a custom exception.

We'll do that in the next two chapters.

---

# Common Beginner Mistakes

## Mistake 1

Using `throw` instead of validation.

Sometimes a simple `if` statement is enough.

Throw exceptions only when the method cannot continue correctly.

---

## Mistake 2

Throwing generic exceptions.

Bad:

```java
throw new Exception("Error");
```

Prefer the most meaningful exception type.

---

## Mistake 3

Writing vague messages.

Bad:

```java
throw new IllegalArgumentException("Wrong.");
```

Better:

```java
throw new IllegalArgumentException(
    "Age cannot be negative."
);
```

Clear messages make debugging much easier.

---

## Mistake 4

Forgetting that `throw` stops execution.

Everything after the `throw` statement is skipped unless the exception is handled elsewhere.

---

# Professional Best Practices

* Validate method arguments at the beginning of the method.
* Use guard clauses to reject invalid input early.
* Throw the most specific exception that describes the problem.
* Write clear, meaningful exception messages.
* Prefer built-in exception types when they accurately represent the failure.
* Create custom exceptions only when they improve the clarity of your domain model.

---

# Guided Exercise 3 — Student Registration

In this exercise, we'll validate a student's age and manually throw an exception if the value is invalid.

For now, we'll use `IllegalArgumentException`. In the next chapters, we'll replace it with a custom `InvalidAgeException`.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
├── model/
│   └── Student.java
└── service/
    └── StudentService.java
```

---

## Step 2 — Create `Student`

```java
package model;

public class Student {

    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public int getAge() {
        return age;
    }

}
```

---

## Step 3 — Create `StudentService`

```java
package service;

import model.Student;

public class StudentService {

    public void register(Student student) {

        if (student.getAge() < 18) {

            throw new IllegalArgumentException(
                "Student must be at least 18 years old."
            );

        }

        System.out.println("Student registered successfully.");

    }

}
```

---

## Step 4 — Test in `Main`

```java
import model.Student;
import service.StudentService;

public class Main {

    public static void main(String[] args) {

        StudentService service = new StudentService();

        try {

            Student student = new Student("Alice", 16);

            service.register(student);

        } catch (IllegalArgumentException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

### Expected Output

```text
Student must be at least 18 years old.
```

### Experiments

Try changing the student's age to:

* `16`
* `18`
* `21`
* `-5`

Observe:

* When is the exception thrown?
* When is the registration successful?
* Which lines execute after the `throw` statement?

---

# Chapter Summary

In this chapter, you learned that:

* `throw` allows you to create and throw exceptions manually.
* Thrown exceptions interrupt the current execution flow immediately.
* Business rules are a common reason to throw exceptions.
* Guard clauses help validate input early and keep methods clean.
* `throw` and `throws` have different purposes.
* Meaningful exception types and messages make applications easier to understand and maintain.

You can now create exceptions yourself.

The next step is learning how to **declare** that a method may throw an exception using the `throws` keyword and how exception propagation works across multiple methods.

---

# ✔️ Next Step

Proceed to **Chapter 9 — `throws`**, where you'll learn how methods declare the exceptions they may produce, how checked exceptions propagate through the call stack, and how to decide where an exception should ultimately be handled.
