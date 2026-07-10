# Chapter 5 — `try` and `catch`

Now that you understand **how exceptions propagate**, it's time to learn how to **handle** them.

This is where Java gives developers the ability to recover from problems instead of allowing the application to terminate.

The two keywords you'll use most often are:

* `try`
* `catch`

Together, they form the foundation of Java's exception handling system.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What `try` does
* What `catch` does
* The execution flow of a `try/catch` block
* How Java matches exceptions to `catch` blocks
* When to use `try/catch`
* When **not** to use `try/catch`
* Common beginner mistakes
* Professional best practices

---

# Why Do We Need `try`?

Without exception handling, an unhandled exception causes the program to stop.

Example:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Program started");

        int result = 10 / 0;

        System.out.println(result);

        System.out.println("Program finished");

    }

}
```

Output:

```text
Program started

Exception in thread "main" java.lang.ArithmeticException: / by zero
```

Notice what happened.

These lines were **never executed**:

```java
System.out.println(result);

System.out.println("Program finished");
```

The exception interrupted the normal execution flow.

---

# The Purpose of `try`

A `try` block tells Java:

> "The code inside this block might throw an exception."

Syntax:

```java
try {

    // risky code

}
```

By itself, a `try` block is incomplete.

Java requires it to be followed by at least one:

* `catch`
* `finally`

or both.

This is **invalid**:

```java
try {

    int result = 10 / 0;

}
```

The compiler reports an error because Java doesn't know what should happen if an exception occurs.

---

# The Purpose of `catch`

A `catch` block tells Java:

> "If a specific type of exception occurs, execute this code."

Syntax:

```java
try {

    // risky code

} catch (ExceptionType e) {

    // recovery code

}
```

The variable (`e` in this example) refers to the exception object that was thrown.

---

# Our First `try/catch`

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Program started");

        try {

            int result = 10 / 0;

            System.out.println(result);

        } catch (ArithmeticException e) {

            System.out.println("Division by zero is not allowed.");

        }

        System.out.println("Program finished");

    }

}
```

Output:

```text
Program started
Division by zero is not allowed.
Program finished
```

This time, the program continued running because the exception was handled.

---

# Execution Flow

Let's examine what happened.

```text
Program starts
      ↓
Enter try block
      ↓
Execute risky code
      ↓
Exception occurs
      ↓
Search matching catch
      ↓
ArithmeticException found
      ↓
Execute catch block
      ↓
Continue after try/catch
```

Notice that Java **did not** continue executing the remaining statements inside the `try` block.

Instead, it immediately jumped to the matching `catch`.

---

# What Happens Inside the `try` Block?

Consider this example.

```java
try {

    System.out.println("A");

    int result = 10 / 0;

    System.out.println("B");

    System.out.println("C");

} catch (ArithmeticException e) {

    System.out.println("Exception handled");

}
```

Output:

```text
A
Exception handled
```

Why weren't `"B"` and `"C"` printed?

Because once an exception is thrown:

* The rest of the `try` block is skipped.
* Java immediately transfers control to the appropriate `catch`.

---

# What If No Exception Occurs?

Suppose we divide by a valid number.

```java
try {

    int result = 10 / 2;

    System.out.println(result);

} catch (ArithmeticException e) {

    System.out.println("Error");

}
```

Output:

```text
5
```

Notice something important.

The `catch` block was completely ignored.

Java only enters a `catch` block if the corresponding exception is actually thrown.

---

# What Does the Exception Variable Contain?

Look at this declaration:

```java
catch (ArithmeticException e)
```

The variable `e` is an object.

It contains valuable information about the exception.

For example:

```java
System.out.println(e.getMessage());
```

Output:

```text
/ by zero
```

You can also print the exception itself.

```java
System.out.println(e);
```

Output:

```text
java.lang.ArithmeticException: / by zero
```

And during debugging, you can print the full stack trace.

```java
e.printStackTrace();
```

Example output:

```text
java.lang.ArithmeticException: / by zero
    at Main.main(Main.java:8)
```

These methods are extremely useful while developing and debugging applications.

---

# Catching Different Exception Types

The type inside `catch` determines which exceptions it can handle.

Example:

```java
catch (ArithmeticException e)
```

Only handles:

```java
ArithmeticException
```

It will **not** catch:

* `NullPointerException`
* `NumberFormatException`
* `IOException`

Each `catch` block is responsible for the type it declares (and its subclasses, due to inheritance).

We'll explore multiple `catch` blocks in the next chapter.

---

# Should Everything Go Inside a `try` Block?

No.

A common beginner mistake is writing:

```java
try {

    System.out.println("Welcome");

    int age = 20;

    int result = 10 / age;

    System.out.println(result);

    System.out.println("Goodbye");

} catch (Exception e) {

    System.out.println("Error");

}
```

Most of this code cannot throw the exception we're interested in.

Professional developers keep `try` blocks as small as practical.

For example:

```java
System.out.println("Welcome");

int age = 20;

try {

    int result = 10 / age;

    System.out.println(result);

} catch (ArithmeticException e) {

    System.out.println("Division by zero.");

}

System.out.println("Goodbye");
```

This makes it much easier to see which operations are actually being protected.

---

# When Should You Use `try/catch`?

Use it when your application can meaningfully recover.

Examples:

* Ask the user for another input.
* Retry an operation.
* Display a helpful message.
* Skip invalid data and continue processing.
* Return to a menu instead of terminating.

---

# When Should You NOT Use `try/catch`?

Do **not** use `try/catch` simply to hide problems.

Bad example:

```java
try {

    int result = 10 / 0;

} catch (Exception e) {

}
```

The exception disappears.

The user gets no explanation.

The developer gets no information.

The application silently ignores an important problem.

This is called an **empty catch block**, and it is considered poor practice.

---

# Common Beginner Mistakes

## Mistake 1

Putting too much code inside a `try`.

Keep `try` blocks focused on operations that may actually throw the exception you're handling.

---

## Mistake 2

Using `catch (Exception e)` for everything.

While sometimes appropriate, catching the most general exception type everywhere can make it harder to understand and handle different failures correctly.

Prefer catching the most specific exception you can reasonably handle.

---

## Mistake 3

Ignoring the exception object.

The exception contains useful debugging information.

Use methods like:

```java
e.getMessage();
```

or, during development:

```java
e.printStackTrace();
```

---

## Mistake 4

Thinking execution resumes inside the `try`.

It doesn't.

Once an exception occurs, the remaining statements in the `try` block are skipped.

Execution continues **after** the `try/catch` block (unless another exception is thrown).

---

# Professional Best Practices

* Catch only exceptions you know how to handle.
* Keep `try` blocks small and focused.
* Write meaningful messages for users when appropriate.
* Use the exception object to aid debugging.
* Never leave `catch` blocks empty.
* Don't use exceptions as a replacement for normal program logic.

---

# Guided Exercise 1 — Division Calculator

Let's build the first exercise for this module.

## Goal

Create a calculator that safely performs division without crashing when the user enters zero as the divisor.

### Step 1 — Create the project structure

```text
src/
├── Main.java
└── service/
    └── CalculatorService.java
```

---

### Step 2 — Create `CalculatorService`

```java
package service;

public class CalculatorService {

    public int divide(int a, int b) {
        return a / b;
    }

}
```

---

### Step 3 — Use `try/catch` in `Main`

```java
import service.CalculatorService;

public class Main {

    public static void main(String[] args) {

        CalculatorService calculator = new CalculatorService();

        try {

            int result = calculator.divide(10, 0);

            System.out.println("Result: " + result);

        } catch (ArithmeticException e) {

            System.out.println("Error: Division by zero is not allowed.");

        }

        System.out.println("Application continues running.");

    }

}
```

### Expected Output

```text
Error: Division by zero is not allowed.
Application continues running.
```

### Try These Variations

Experiment by changing the divisor:

* `2`
* `5`
* `1`
* `0`
* `-2`

Observe:

* When is the `catch` block executed?
* When is it skipped?
* Does the program continue after the `try/catch` block in every case?

Understanding these execution paths is key before moving on.

---

# Chapter Summary

In this chapter, you learned that:

* `try` marks code that may throw an exception.
* `catch` handles a matching exception type.
* When an exception occurs, the rest of the `try` block is skipped.
* If no exception occurs, the `catch` block is ignored.
* The exception object provides detailed information about the failure.
* `try/catch` should be used only when your application can respond meaningfully to the problem.
* Small, focused `try` blocks make code easier to read and maintain.

You now know how to handle a single exception.

The next step is learning how to handle **multiple different exception types** in a clean and organized way.

---

# ✔️ Next Step

Proceed to **Chapter 6 — Multiple `catch` Blocks**, where you'll learn how Java chooses between different handlers, why the order of `catch` blocks matters, and how inheritance affects exception matching.
