# Chapter 6 — Multiple `catch` Blocks

In the previous chapter, we learned how to handle **one specific exception** using a single `catch` block.

However, real applications rarely fail in only one way.

A single piece of code might throw several different exceptions, each requiring a different response.

Java allows us to write **multiple `catch` blocks**, each responsible for handling a specific type of exception.

This makes our code clearer, more maintainable, and more precise.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* How multiple `catch` blocks work
* How Java chooses the correct `catch`
* Why the order of `catch` blocks matters
* How inheritance affects exception matching
* Multi-catch syntax (`|`)
* Best practices for organizing exception handlers
* Common beginner mistakes

---

# Why Multiple `catch` Blocks?

Imagine a simple program that:

1. Converts text into a number.
2. Divides another number by the converted value.

Two different things can go wrong:

* The text is not a valid number.
* The number is zero.

These are different problems and should have different messages.

Example:

```java
String input = "0";

int number = Integer.parseInt(input);

System.out.println(10 / number);
```

Possible exceptions:

* `NumberFormatException`
* `ArithmeticException`

One generic message would not be very helpful.

---

# Multiple `catch` Syntax

Java allows several `catch` blocks after a single `try`.

```java
try {

    // risky code

} catch (FirstException e) {

    // handle first exception

} catch (SecondException e) {

    // handle second exception

}
```

Each `catch` handles a different exception type.

---

# Example 1 — Invalid Number

```java
public class Main {

    public static void main(String[] args) {

        try {

            int number = Integer.parseInt("abc");

            System.out.println(number);

        } catch (NumberFormatException e) {

            System.out.println("Invalid number.");

        } catch (ArithmeticException e) {

            System.out.println("Division by zero.");

        }

    }

}
```

Output:

```text
Invalid number.
```

Java skipped the second `catch` because the exception was a `NumberFormatException`.

---

# Example 2 — Division by Zero

```java
public class Main {

    public static void main(String[] args) {

        try {

            int number = Integer.parseInt("0");

            System.out.println(10 / number);

        } catch (NumberFormatException e) {

            System.out.println("Invalid number.");

        } catch (ArithmeticException e) {

            System.out.println("Division by zero.");

        }

    }

}
```

Output:

```text
Division by zero.
```

Now Java executed the second `catch`.

---

# How Java Chooses a `catch`

Java checks the `catch` blocks **from top to bottom**.

As soon as it finds the **first compatible handler**, it executes it and ignores all remaining `catch` blocks.

Flow:

```text
Exception thrown
       ↓
First catch?
       ↓
Matches?
   Yes → Execute it
   No
       ↓
Second catch?
       ↓
Matches?
   Yes → Execute it
   No
       ↓
Continue searching...
```

Only **one** `catch` block executes for a given exception.

---

# The Importance of Order

Because Java searches from top to bottom, the order of `catch` blocks is extremely important.

Consider this:

```java
try {

    int number = Integer.parseInt("abc");

} catch (Exception e) {

    System.out.println("General exception.");

} catch (NumberFormatException e) {

    System.out.println("Invalid number.");

}
```

This **does not compile**.

Why?

Because `Exception` is the superclass of `NumberFormatException`.

The first `catch` already catches every `NumberFormatException`.

The second `catch` can never be reached.

The compiler reports an **unreachable catch block**.

---

# Correct Ordering

Always place **more specific exceptions first**.

```java
try {

    int number = Integer.parseInt("abc");

} catch (NumberFormatException e) {

    System.out.println("Invalid number.");

} catch (Exception e) {

    System.out.println("General exception.");

}
```

This works because:

1. Java first checks the specific exception.
2. If it doesn't match, it falls back to the more general handler.

---

# Understanding Inheritance

Remember from previous modules:

```text
Exception
        ↑
RuntimeException
        ↑
NumberFormatException
```

Since `NumberFormatException` **is a** `Exception`, this handler also works:

```java
catch (Exception e)
```

But you lose the ability to distinguish the exact problem.

Whenever possible, catch the most specific exception that you can meaningfully handle.

---

# Multi-Catch (`|`)

Sometimes two different exceptions should be handled exactly the same way.

Instead of duplicating code:

```java
catch (ArithmeticException e) {

    System.out.println("Invalid operation.");

}

catch (NumberFormatException e) {

    System.out.println("Invalid operation.");

}
```

Java allows a **multi-catch**:

```java
catch (ArithmeticException | NumberFormatException e) {

    System.out.println("Invalid operation.");

}
```

The `|` symbol means:

> Handle either exception using the same code.

This reduces duplication and improves readability.

---

# When Should You Use Multi-Catch?

Use it when:

* The recovery logic is identical.
* The exceptions have the same meaning in your application.
* You don't need different messages or actions.

Avoid it when different exception types require different responses.

---

# Example

```java
try {

    int number = Integer.parseInt("abc");

    System.out.println(10 / number);

} catch (ArithmeticException | NumberFormatException e) {

    System.out.println("Invalid user input.");

}
```

Whether parsing fails or division by zero occurs, the same message is shown.

---

# Can Multiple Exceptions Occur?

Consider this code:

```java
int number = Integer.parseInt("abc");

System.out.println(10 / number);
```

Could both exceptions happen?

No.

The first exception immediately interrupts execution.

If parsing fails, division is never attempted.

Only **one exception** is active at a time.

---

# Common Beginner Mistakes

## Mistake 1

Placing `Exception` before specific exceptions.

Incorrect:

```java
catch (Exception e)
```

before

```java
catch (NumberFormatException e)
```

Always catch subclasses first.

---

## Mistake 2

Using `Exception` everywhere.

This hides useful information.

Instead of:

```java
catch (Exception e)
```

Prefer:

```java
catch (NumberFormatException e)
```

or

```java
catch (ArithmeticException e)
```

whenever possible.

---

## Mistake 3

Duplicating identical code.

If two exceptions are handled exactly the same way, consider using a multi-catch.

---

## Mistake 4

Expecting multiple `catch` blocks to execute.

Only the **first matching** `catch` block runs.

The others are skipped.

---

# Professional Best Practices

* Catch the most specific exception possible.
* Order `catch` blocks from most specific to most general.
* Use multi-catch only when the handling logic is truly identical.
* Avoid generic `catch (Exception e)` unless you have a clear reason.
* Keep each `catch` focused on recovering from a particular problem.

---

# Guided Exercise 2 — Number Parser

In this exercise, we'll safely convert user input into an integer and handle two possible problems:

* Invalid numeric input.
* Division by zero.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
└── service/
    └── ParserService.java
```

---

## Step 2 — Create `ParserService`

```java
package service;

public class ParserService {

    public int parse(String value) {
        return Integer.parseInt(value);
    }

}
```

---

## Step 3 — Test Multiple Exceptions

```java
import service.ParserService;

public class Main {

    public static void main(String[] args) {

        ParserService parser = new ParserService();

        try {

            int number = parser.parse("0");

            System.out.println(100 / number);

        } catch (NumberFormatException e) {

            System.out.println("Please enter a valid number.");

        } catch (ArithmeticException e) {

            System.out.println("Cannot divide by zero.");

        }

        System.out.println("Program finished.");

    }

}
```

---

## Experiments

Try changing:

```java
parser.parse("0");
```

to:

```java
parser.parse("25");
```

Then:

```java
parser.parse("abc");
```

Observe:

* Which `catch` executes?
* Does the program continue afterward?
* Which lines are skipped after an exception?

Understanding these execution paths will reinforce how Java selects exception handlers.

---

# Chapter Summary

In this chapter, you learned that:

* A single `try` block can have multiple `catch` blocks.
* Java checks `catch` blocks from top to bottom.
* Only the first compatible `catch` executes.
* More specific exception types must come before more general ones.
* Multi-catch (`|`) allows different exception types to share the same handling logic.
* Catching specific exceptions produces clearer, more maintainable code.

You now know how to handle different kinds of failures appropriately.

The next step is learning about a special block that runs **whether an exception occurs or not**.

---

# ✔️ Next Step

Proceed to **Chapter 7 — `finally`**, where you'll learn how to guarantee that cleanup code always executes, even when exceptions interrupt the normal flow of your program.
