# Chapter 11 — Java Built-in Exceptions

Throughout this module, you've already encountered several Java exceptions.

Now it's time to study the most common ones in detail.

Professional developers recognize these exceptions almost immediately because they appear frequently during development.

Understanding:

* what causes them,
* how to prevent them,
* and when to handle them,

will make debugging much easier.

Remember:

> **An exception is not the problem—it is Java telling you that a problem has already occurred.**

Your goal is to understand **why** the exception happened.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* The most common Java exceptions
* What causes each one
* How to reproduce them
* How to avoid them
* Whether they are checked or unchecked
* Best practices for preventing them

---

# The Exceptions We'll Study

| Exception                        | Checked? | Common Cause                          |
| -------------------------------- | -------- | ------------------------------------- |
| `NullPointerException`           | ❌ No     | Using a null reference                |
| `ArithmeticException`            | ❌ No     | Invalid arithmetic operation          |
| `ArrayIndexOutOfBoundsException` | ❌ No     | Invalid array index                   |
| `IllegalArgumentException`       | ❌ No     | Invalid method argument               |
| `NumberFormatException`          | ❌ No     | Invalid numeric conversion            |
| `IOException`                    | ✅ Yes    | File or input/output operation failed |

Notice something interesting.

Only one exception in this chapter is checked:

```text
IOException
```

The others are all unchecked exceptions.

---

# 1. NullPointerException (NPE)

This is probably the most famous Java exception.

It occurs when you try to use a reference that points to `null`.

Example:

```java
String name = null;

System.out.println(name.length());
```

Output:

```text
Exception in thread "main"
java.lang.NullPointerException
```

Why?

Because there is **no object**.

The variable exists.

The object does not.

---

## Memory Visualization

```text
String name

↓

null
```

There is no `String` object.

Trying to call:

```java
name.length()
```

is impossible.

---

## Correct Version

```java
String name = "Alice";

System.out.println(name.length());
```

Output:

```text
5
```

---

## Prevention

Always verify references before using them.

Example:

```java
if (name != null) {

    System.out.println(name.length());

}
```

---

## Best Practice

Instead of catching `NullPointerException`, prevent it by writing defensive code.

---

# 2. ArithmeticException

Occurs when Java detects an invalid arithmetic operation.

Most common example:

```java
int result = 10 / 0;
```

Output:

```text
java.lang.ArithmeticException: / by zero
```

---

## Prevention

Validate the divisor first.

```java
if (divisor != 0) {

    System.out.println(number / divisor);

}
```

---

## Best Practice

Validate values before performing calculations.

---

# 3. ArrayIndexOutOfBoundsException

Occurs when accessing an invalid array index.

Example:

```java
int[] numbers = {10, 20, 30};

System.out.println(numbers[5]);
```

Output:

```text
java.lang.ArrayIndexOutOfBoundsException
```

The valid indexes are:

```text
0
1
2
```

Index:

```text
5
```

does not exist.

---

## Prevention

Always check:

```java
if (index >= 0 && index < numbers.length)
```

before accessing an array.

---

## Best Practice

Whenever iterating through arrays, use:

```java
numbers.length
```

instead of hardcoding indexes.

Example:

```java
for (int i = 0; i < numbers.length; i++) {

    System.out.println(numbers[i]);

}
```

---

# 4. IllegalArgumentException

This exception usually indicates that a method received an invalid argument.

Example:

```java
public void setAge(int age) {

    if (age < 0) {

        throw new IllegalArgumentException(
            "Age cannot be negative."
        );

    }

}
```

Notice that Java didn't throw this exception automatically.

We threw it intentionally because the argument violated a business rule.

---

## Prevention

Validate arguments at the beginning of methods.

This is one of the most common uses of **guard clauses**.

---

# 5. NumberFormatException

Occurs when converting invalid text into a number.

Example:

```java
int number = Integer.parseInt("abc");
```

Output:

```text
java.lang.NumberFormatException
```

Java expected:

```text
123
```

but received:

```text
abc
```

---

## Correct Example

```java
int number = Integer.parseInt("123");
```

---

## Prevention

Whenever user input is involved:

* validate it,
* or use `try/catch`.

Example:

```java
try {

    int number = Integer.parseInt(input);

} catch (NumberFormatException e) {

    System.out.println("Please enter a valid number.");

}
```

---

# 6. IOException

Unlike the previous exceptions:

```text
IOException
```

is **checked**.

It usually occurs during:

* reading files,
* writing files,
* network communication,
* streams,
* input/output operations.

Example signature:

```java
public void loadData()
        throws IOException {

}
```

We won't work deeply with files in this module.

The important point is understanding that Java requires checked exceptions to be:

* handled, or
* declared.

---

# Quick Comparison

| Exception                        | Cause                     | Prevention          |
| -------------------------------- | ------------------------- | ------------------- |
| `NullPointerException`           | Null reference            | Check for `null`    |
| `ArithmeticException`            | Division by zero          | Validate divisor    |
| `ArrayIndexOutOfBoundsException` | Invalid index             | Check array bounds  |
| `IllegalArgumentException`       | Invalid parameter         | Validate arguments  |
| `NumberFormatException`          | Invalid numeric string    | Validate user input |
| `IOException`                    | File/Input-Output failure | Handle or declare   |

---

# Which Exceptions Should We Catch?

A common beginner question is:

> "Should I catch every exception?"

No.

Professional developers usually try to **prevent** exceptions before they happen.

Examples:

Instead of:

```java
try {

    int result = number / divisor;

} catch (ArithmeticException e) {

}
```

Prefer:

```java
if (divisor != 0) {

    int result = number / divisor;

}
```

Validation is often cleaner than relying on exceptions.

---

# Exception Prevention vs Exception Handling

Good software uses both.

### Prevention

* Validate input
* Validate indexes
* Validate arguments
* Check for null

### Handling

* Recover from invalid user input
* Retry operations
* Inform the user
* Log or propagate failures (in larger applications)

---

# Common Beginner Mistakes

## Mistake 1

Using exceptions instead of validation.

Example:

```java
try {

    array[index];

} catch (...) {

}
```

Better:

```java
if (index < array.length)
```

---

## Mistake 2

Ignoring stack traces.

The exception type usually tells you exactly where to begin debugging.

---

## Mistake 3

Catching generic `Exception`.

Catch the specific exception you expect whenever possible.

---

## Mistake 4

Thinking exceptions are "bad."

Exceptions are actually useful.

They help detect bugs early and prevent invalid application states.

---

# Professional Best Practices

* Prevent predictable exceptions with validation.
* Handle recoverable situations gracefully.
* Let unexpected exceptions propagate when appropriate.
* Use meaningful exception messages.
* Learn the common built-in exceptions—you'll encounter them frequently.

---

# Guided Exercise 5 — Login System

In this exercise, you'll combine validation with a custom exception.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
├── service/
│   └── LoginService.java
└── exception/
    └── InvalidLoginException.java
```

---

## Step 2 — Create `InvalidLoginException`

```java
package exception;

public class InvalidLoginException
        extends RuntimeException {

    public InvalidLoginException(String message) {

        super(message);

    }

}
```

---

## Step 3 — Create `LoginService`

```java
package service;

import exception.InvalidLoginException;

public class LoginService {

    public void login(String username, String password) {

        if (username.isBlank()) {

            throw new InvalidLoginException(
                "Username cannot be empty."
            );

        }

        if (password.isBlank()) {

            throw new InvalidLoginException(
                "Password cannot be empty."
            );

        }

        System.out.println("Login successful.");

    }

}
```

---

## Step 4 — Test in `Main`

```java
import exception.InvalidLoginException;
import service.LoginService;

public class Main {

    public static void main(String[] args) {

        LoginService service = new LoginService();

        try {

            service.login("", "123456");

        } catch (InvalidLoginException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

### Expected Output

```text
Username cannot be empty.
```

### Experiments

Try:

```java
service.login("admin", "");
```

Then:

```java
service.login("admin", "123456");
```

Observe:

* Which validations execute?
* When is the exception thrown?
* When does the login succeed?

---

# Chapter Summary

In this chapter, you learned that:

* Java includes many built-in exceptions for common programming errors.
* Most frequently encountered exceptions are unchecked.
* `IOException` is one of the most common checked exceptions.
* Validation prevents many exceptions before they occur.
* Exception handling complements validation by allowing applications to recover gracefully.
* Understanding common exceptions makes debugging faster and more effective.

You now have a solid understanding of both built-in and custom exceptions, along with the defensive programming techniques used to build reliable applications.

---

# ✔️ Next Step

Proceed to **Chapter 12 — Final Project: Banking System with Exception Handling**, where you'll progressively build a complete console-based banking application that applies everything you've learned in this module: custom exceptions, `try/catch`, `finally`, `throw`, `throws`, exception propagation, validation, and proper project organization.
