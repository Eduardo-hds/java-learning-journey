# Chapter 9 — `throws`

In the previous chapter, you learned how to **throw** an exception.

Now we'll learn how a method can **declare** that it may throw an exception.

This is the purpose of the `throws` keyword.

At first glance, `throw` and `throws` look very similar.

In reality, they solve completely different problems.

Understanding this distinction is essential, especially when working with **checked exceptions**.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What `throws` is
* Why Java requires it for checked exceptions
* The difference between `throw` and `throws`
* How exception propagation works across methods
* Where exceptions should be handled
* When to declare exceptions
* When not to declare exceptions
* Professional best practices

---

# What is `throws`?

The `throws` keyword is used in a method declaration to tell callers:

> **"This method might throw one or more exceptions. If you call it, you must be prepared to deal with them."**

Unlike `throw`, `throws` does **not** create an exception.

It simply declares that one may occur.

Basic syntax:

```java
public void readFile() throws IOException {

}
```

Notice that no exception is thrown here.

The method is only making a promise about its possible behavior.

---

# `throw` vs `throws`

Let's compare them again.

| `throw`                          | `throws`                                      |
| -------------------------------- | --------------------------------------------- |
| Throws an exception immediately  | Declares that a method may throw an exception |
| Used inside a method body        | Used in the method signature                  |
| Stops execution                  | Does not stop execution                       |
| Creates or rethrows an exception | Documents and propagates exceptions           |

Example:

```java
throw new IllegalArgumentException("Invalid age.");
```

versus

```java
public void save() throws IOException {

}
```

These keywords often appear together, but they serve different purposes.

---

# Why Does `throws` Exist?

Imagine a method that reads a file.

Many things can go wrong:

* The file doesn't exist.
* The file is locked.
* The user lacks permission.
* The disk is unavailable.

The method itself may not know how to recover.

Instead of handling every problem internally, it can pass the responsibility to its caller.

That's exactly what `throws` allows.

---

# A Simple Example

```java
public void validateAge(int age) throws IllegalArgumentException {

    if (age < 0) {

        throw new IllegalArgumentException(
            "Age cannot be negative."
        );

    }

}
```

Although this compiles, declaring an unchecked exception like `IllegalArgumentException` with `throws` is usually unnecessary because the compiler does not require callers to handle unchecked exceptions.

The primary purpose of `throws` is with **checked exceptions**.

---

# Exception Propagation

Consider three methods.

```text
main()
    ↓
registerStudent()
    ↓
validateAge()
```

Suppose:

```java
validateAge()
```

throws an exception.

If it doesn't handle it, Java propagates the exception upward.

Flow:

```text
validateAge()
        ↑
registerStudent()
        ↑
main()
```

Each method has a choice:

* Handle the exception.
* Declare it with `throws` and pass it to its caller.

---

# Propagation Example

```java
public static void main(String[] args) {

    registerStudent();

}

public static void registerStudent() {

    validateAge(-5);

}

public static void validateAge(int age) {

    if (age < 0) {

        throw new IllegalArgumentException(
            "Age cannot be negative."
        );

    }

}
```

Execution:

```text
validateAge()
        ↑
registerStudent()
        ↑
main()
        ↑
JVM
```

Since nobody catches the exception, it eventually reaches the JVM, which terminates the application and prints the stack trace.

---

# Declaring Checked Exceptions

Now imagine a checked exception such as:

```java
IOException
```

A method may declare:

```java
public void loadData() throws IOException {

    // file operations

}
```

Any code that calls `loadData()` must now either:

* Handle the exception with `try/catch`, or
* Declare it with `throws` as well.

This is how checked exceptions propagate through an application.

---

# Passing Responsibility

Imagine these methods:

```text
main()
    ↓
service()
    ↓
repository()
```

`repository()` throws a checked exception.

It may decide not to handle it.

Instead:

```java
public void repository() throws IOException {

}
```

Then:

```java
public void service() throws IOException {

    repository();

}
```

Finally:

```java
public static void main(String[] args) {

    try {

        service();

    } catch (IOException e) {

        System.out.println("Unable to load data.");

    }

}
```

Here, only `main()` actually handles the exception.

The intermediate methods simply propagated it.

---

# Where Should Exceptions Be Handled?

This is one of the most important design decisions in Java.

There is no universal rule, but a good guideline is:

> Handle an exception at the level that has enough context to recover from it.

Examples:

### Good

A user enters invalid input.

The user interface can ask for another value.

---

### Good

A service detects an invalid bank withdrawal.

The caller can inform the customer and request a different amount.

---

### Poor

A low-level utility catches every exception, prints a message, and hides the problem.

The higher layers lose the opportunity to make an informed decision.

---

# Declaring Multiple Exceptions

A method can declare more than one exception.

Example:

```java
public void process()
        throws IOException, ClassNotFoundException {

}
```

The caller must consider all declared checked exceptions.

---

# Can We Use `throws` Without `throw`?

Yes.

A method can declare an exception even if the exception is actually thrown by another method it calls.

Example:

```java
public void service() throws IOException {

    repository();

}
```

The `service()` method didn't throw the exception itself.

It simply allowed it to propagate.

---

# Can We Throw Without `throws`?

Yes.

Unchecked exceptions do not require a `throws` declaration.

Example:

```java
public void validate(int age) {

    if (age < 0) {

        throw new IllegalArgumentException(
            "Invalid age."
        );

    }

}
```

This compiles because `IllegalArgumentException` is an unchecked exception.

---

# Common Beginner Mistakes

## Mistake 1

Thinking `throws` throws an exception.

It doesn't.

It only declares that an exception may occur.

---

## Mistake 2

Adding `throws Exception` to every method.

This hides useful information.

Instead, declare the specific checked exceptions that callers need to know about.

---

## Mistake 3

Handling exceptions too early.

Sometimes the current method cannot recover.

In those cases, let the exception propagate to a higher level.

---

## Mistake 4

Ignoring checked exceptions.

The compiler won't allow this.

You must either handle them or declare them.

---

# Professional Best Practices

* Use `throws` primarily for checked exceptions.
* Let exceptions propagate until a layer can handle them meaningfully.
* Declare specific exception types instead of generic `Exception`.
* Avoid unnecessary `throws` declarations for unchecked exceptions.
* Keep exception handling close to where recovery is possible.

---

# Guided Exercise 6 — Exception Propagation

In this exercise, we'll observe how an exception travels through multiple methods before being handled.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
└── service/
    └── RegistrationService.java
```

---

## Step 2 — Create `RegistrationService`

```java
package service;

public class RegistrationService {

    public void register(int age) {

        validateAge(age);

        System.out.println("Registration completed.");

    }

    private void validateAge(int age) {

        if (age < 18) {

            throw new IllegalArgumentException(
                "Student must be at least 18 years old."
            );

        }

    }

}
```

---

## Step 3 — Test in `Main`

```java
import service.RegistrationService;

public class Main {

    public static void main(String[] args) {

        RegistrationService service = new RegistrationService();

        try {

            service.register(16);

        } catch (IllegalArgumentException e) {

            System.out.println("Registration failed.");

            System.out.println(e.getMessage());

        }

        System.out.println("Program continues.");

    }

}
```

### Expected Output

```text
Registration failed.
Student must be at least 18 years old.
Program continues.
```

### Follow the Flow

Observe the sequence:

```text
main()
    ↓
register()
    ↓
validateAge()
         X throw
    ↑
register()
    ↑
main()
    ↓
catch
```

Even though `validateAge()` throws the exception, it is `main()` that ultimately handles it.

This is exception propagation in action.

---

# Chapter Summary

In this chapter, you learned that:

* `throws` declares that a method may produce an exception.
* `throw` and `throws` have completely different purposes.
* Checked exceptions are the primary reason for using `throws`.
* Exceptions automatically propagate up the call stack until they are handled or reach the JVM.
* A method should only handle an exception if it can meaningfully recover from it.
* Clear exception propagation leads to cleaner and more maintainable application design.

You now understand how exceptions move between methods and how Java communicates potential failures through method signatures.

---

# ✔️ Next Step

Proceed to **Chapter 10 — Creating Custom Exceptions**, where you'll build your own exception classes (`InvalidAgeException`, `InsufficientFundsException`, and `InvalidLoginException`), organize them inside a dedicated `exception` package, and learn when to extend `Exception` versus `RuntimeException`.
