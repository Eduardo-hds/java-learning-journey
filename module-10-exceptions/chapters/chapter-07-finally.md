# Chapter 7 — `finally`

So far, you've learned how to:

* Detect exceptions
* Handle exceptions with `catch`
* Handle different exception types

But there is still an important question:

> **How can we guarantee that certain code always runs, regardless of whether an exception occurs?**

Imagine you open a file, connect to a database, or reserve some resource.

Even if an exception occurs, you still need to clean up those resources.

This is exactly the purpose of the `finally` block.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What `finally` is
* When `finally` executes
* Why cleanup is important
* The execution order of `try`, `catch`, and `finally`
* Situations where `finally` is commonly used
* Common mistakes
* Professional best practices

---

# Why Do We Need `finally`?

Suppose your program performs three steps:

1. Open a resource.
2. Perform an operation.
3. Close the resource.

Without `finally`, an exception might prevent step 3 from executing.

Example:

```java
System.out.println("Opening resource...");

int result = 10 / 0;

System.out.println("Closing resource...");
```

Output:

```text
Opening resource...

Exception in thread "main" java.lang.ArithmeticException: / by zero
```

Notice what happened.

The resource was "opened" but never "closed."

In real applications, this can lead to:

* Memory leaks
* Locked files
* Open network connections
* Database connections remaining active
* Resource exhaustion

---

# The Purpose of `finally`

A `finally` block contains code that Java executes **after** the `try` (and any matching `catch`), regardless of whether an exception occurred.

Basic syntax:

```java
try {

    // risky code

} catch (Exception e) {

    // handle exception

} finally {

    // cleanup code

}
```

Think of `finally` as Java saying:

> "No matter what happens above, execute this block before leaving."

---

# Example 1 — Exception Occurs

```java
public class Main {

    public static void main(String[] args) {

        try {

            System.out.println("Inside try");

            int result = 10 / 0;

        } catch (ArithmeticException e) {

            System.out.println("Exception handled");

        } finally {

            System.out.println("Finally executed");

        }

    }

}
```

Output:

```text
Inside try
Exception handled
Finally executed
```

Even though an exception occurred, `finally` still executed.

---

# Example 2 — No Exception

```java
try {

    System.out.println("Inside try");

    int result = 10 / 2;

    System.out.println(result);

} catch (ArithmeticException e) {

    System.out.println("Exception");

} finally {

    System.out.println("Finally");

}
```

Output:

```text
Inside try
5
Finally
```

No exception happened.

The `catch` block was skipped.

The `finally` block still executed.

---

# Execution Flow

## Case 1 — No Exception

```text
Enter try
      ↓
Execute try
      ↓
Skip catch
      ↓
Execute finally
      ↓
Continue program
```

---

## Case 2 — Exception Handled

```text
Enter try
      ↓
Exception occurs
      ↓
Execute matching catch
      ↓
Execute finally
      ↓
Continue program
```

---

## Case 3 — Exception Not Handled

```text
Enter try
      ↓
Exception occurs
      ↓
No matching catch
      ↓
Execute finally
      ↓
Exception propagates
```

This is a very important point.

Even if the exception is **not handled**, Java still executes the `finally` block before continuing the exception propagation.

---

# Real-World Analogy

Imagine borrowing a library book.

You might:

1. Read the book successfully.
2. Stop reading because you're interrupted.

Regardless of what happened, you still need to return the book.

The act of returning the book is like the `finally` block.

It happens no matter how the previous steps ended.

---

# Simulating Resource Cleanup

Let's simulate opening and closing a resource.

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Opening connection");

        try {

            System.out.println("Performing operation");

            int result = 10 / 0;

        } catch (ArithmeticException e) {

            System.out.println("Operation failed");

        } finally {

            System.out.println("Closing connection");

        }

    }

}
```

Output:

```text
Opening connection
Performing operation
Operation failed
Closing connection
```

The cleanup always happens.

---

# Can We Use `finally` Without `catch`?

Yes.

A `try` block may be followed directly by `finally`.

Example:

```java
try {

    System.out.println("Working...");

} finally {

    System.out.println("Cleanup");

}
```

This is valid.

However, if an exception occurs inside the `try`, it will still propagate after `finally` executes because there is no `catch` to handle it.

---

# Can We Use `catch` Without `finally`?

Yes.

We've already done this throughout the previous chapters.

```java
try {

    // code

} catch (Exception e) {

    // recovery

}
```

Both forms are perfectly valid.

Use `finally` only when you have cleanup work that must always be performed.

---

# What Belongs in `finally`?

Typical cleanup tasks include:

* Closing files
* Closing scanners
* Closing network connections
* Releasing locks
* Cleaning temporary resources
* Printing "cleanup complete" messages in learning exercises

Notice that these are **cleanup activities**, not business logic.

---

# What Should NOT Go in `finally`?

Avoid putting normal application logic inside `finally`.

Bad example:

```java
finally {

    processPayment();

}
```

If `processPayment()` represents the main purpose of your application, it belongs in the normal execution flow, not in cleanup.

`finally` should focus on restoring or releasing resources.

---

# A Note About Modern Java

In modern Java, many resources are managed using **try-with-resources**, which automatically closes resources.

Example:

```java
try (Scanner scanner = new Scanner(System.in)) {

    // use scanner

}
```

The scanner is closed automatically.

We won't cover this feature in detail in this module because our focus is on understanding the fundamentals of exception handling.

Once you fully understand `finally`, learning try-with-resources becomes much easier.

---

# Common Beginner Mistakes

## Mistake 1

Thinking `finally` only runs when an exception occurs.

It runs whether an exception occurs or not.

---

## Mistake 2

Putting business logic in `finally`.

Keep `finally` focused on cleanup.

---

## Mistake 3

Assuming `finally` catches exceptions.

It doesn't.

It simply guarantees execution.

Exception handling still belongs in `catch`.

---

## Mistake 4

Forgetting that exceptions can continue propagating after `finally`.

If no matching `catch` exists, Java executes `finally` first, then continues searching for a handler.

---

# Professional Best Practices

* Use `finally` for cleanup, not business logic.
* Keep `finally` blocks short and focused.
* Avoid writing code in `finally` that can itself throw exceptions unless absolutely necessary.
* Prefer automatic resource management (try-with-resources) for classes that support it, but understand `finally` first.
* Remember that cleanup is part of writing reliable software.

---

# Guided Exercise 7 — Finally Block Practice

## Goal

Simulate opening and closing a resource while demonstrating that cleanup always occurs.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
└── service/
    └── ResourceService.java
```

---

## Step 2 — Create `ResourceService`

```java
package service;

public class ResourceService {

    public void performOperation() {

        System.out.println("Resource opened.");

        try {

            System.out.println("Performing operation...");

            int result = 10 / 0;

        } finally {

            System.out.println("Resource closed.");

        }

    }

}
```

---

## Step 3 — Test in `Main`

```java
import service.ResourceService;

public class Main {

    public static void main(String[] args) {

        ResourceService service = new ResourceService();

        try {

            service.performOperation();

        } catch (ArithmeticException e) {

            System.out.println("Main handled the exception.");

        }

        System.out.println("Program finished.");

    }

}
```

### Expected Output

```text
Resource opened.
Performing operation...
Resource closed.
Main handled the exception.
Program finished.
```

Observe the order carefully:

1. The resource opens.
2. The operation fails.
3. The `finally` block closes the resource.
4. The exception propagates to `Main`.
5. `Main` handles the exception.
6. The program continues.

This demonstrates both **cleanup** and **exception propagation** working together.

---

# Chapter Summary

In this chapter, you learned that:

* `finally` executes whether an exception occurs or not.
* It is primarily used for cleanup operations.
* `finally` runs after the `try` block and after any matching `catch`.
* If no exception is caught, `finally` still executes before the exception continues propagating.
* Modern Java often uses try-with-resources, but understanding `finally` is the foundation.

You now know how to guarantee cleanup regardless of success or failure.

---

# ✔️ Next Step

Proceed to **Chapter 8 — `throw`**, where you'll learn how to intentionally create and throw exceptions yourself, allowing your code to enforce business rules such as invalid ages, insufficient funds, or invalid account operations.
