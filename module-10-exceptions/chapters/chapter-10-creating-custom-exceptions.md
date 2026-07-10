# Chapter 10 — Creating Custom Exceptions

Throughout this module, we've worked with Java's built-in exceptions such as:

* `IllegalArgumentException`
* `ArithmeticException`
* `NumberFormatException`
* `NullPointerException`

These exceptions are useful, but they cannot describe every problem in your application.

Imagine you're developing a banking system.

If a withdrawal exceeds the available balance, which exception should you use?

```java
throw new IllegalArgumentException("...");
```

It works...

But it doesn't clearly describe the business problem.

A much better solution is:

```java
throw new InsufficientFundsException(
    "Insufficient balance for this withdrawal."
);
```

The exception name itself explains what happened.

This is why professional applications frequently create **custom exceptions**.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* Why custom exceptions exist
* How to create your own exception classes
* The difference between extending `Exception` and `RuntimeException`
* Where custom exceptions belong in a project
* How to throw and catch custom exceptions
* Best practices for designing exception classes

---

# Why Create Custom Exceptions?

Suppose we have this code:

```java
if (balance < amount) {

    throw new IllegalArgumentException(
        "Invalid operation."
    );

}
```

Technically correct.

But imagine reading this six months later.

What does:

```java
IllegalArgumentException
```

tell you?

Not much.

Now compare it with:

```java
throw new InsufficientFundsException(
    "Balance: $200, Withdrawal: $500."
);
```

The exception type itself communicates the business rule.

This makes the code easier to understand and maintain.

---

# Domain Exceptions

Custom exceptions usually represent **business rules**, also called **domain rules**.

Examples:

```text
InvalidAgeException
```

```text
InsufficientFundsException
```

```text
InvalidLoginException
```

```text
ProductOutOfStockException
```

```text
DuplicateEmailException
```

These exceptions describe your application's domain rather than technical problems.

---

# Project Organization

Professional Java projects typically organize custom exceptions in their own package.

```text
src/
│
├── Main.java
│
├── model/
│
├── service/
│
├── exception/
│     ├── InvalidAgeException.java
│     ├── InvalidLoginException.java
│     └── InsufficientFundsException.java
│
└── util/
```

Why?

Because exceptions represent a separate responsibility.

Keeping them together makes projects easier to navigate as they grow.

---

# Creating Your First Custom Exception

Let's begin with:

```text
InvalidAgeException
```

Create:

```text
src/
└── exception/
      └── InvalidAgeException.java
```

Implementation:

```java
package exception;

public class InvalidAgeException extends Exception {

    public InvalidAgeException(String message) {

        super(message);

    }

}
```

This is a checked exception because it extends:

```java
Exception
```

---

# Understanding `super(message)`

Notice this line:

```java
super(message);
```

Remember from the inheritance module:

* `super` calls the constructor of the parent class.
* The parent class here is `Exception`.

Conceptually:

```text
InvalidAgeException
        ↓
Exception
        ↓
Throwable
        ↓
Object
```

The message is stored by the parent class so it can later be retrieved with:

```java
e.getMessage();
```

---

# Throwing Our Custom Exception

Suppose we validate a student's age.

```java
package service;

import exception.InvalidAgeException;

public class StudentService {

    public void register(int age)
            throws InvalidAgeException {

        if (age < 18) {

            throw new InvalidAgeException(
                "Student must be at least 18 years old."
            );

        }

        System.out.println("Student registered.");

    }

}
```

Notice that:

* We throw our own exception.
* Because it extends `Exception`, the method declares it with `throws`.

---

# Catching the Custom Exception

```java
import exception.InvalidAgeException;
import service.StudentService;

public class Main {

    public static void main(String[] args) {

        StudentService service = new StudentService();

        try {

            service.register(16);

        } catch (InvalidAgeException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

Output:

```text
Student must be at least 18 years old.
```

From Java's perspective, this works exactly like any built-in exception.

---

# Creating an Unchecked Exception

Now let's create:

```text
InvalidLoginException
```

Implementation:

```java
package exception;

public class InvalidLoginException
        extends RuntimeException {

    public InvalidLoginException(String message) {

        super(message);

    }

}
```

Notice the difference.

Instead of extending:

```java
Exception
```

we extend:

```java
RuntimeException
```

This makes it an **unchecked exception**.

Methods that throw it do **not** need a `throws` declaration.

---

# Example

```java
public void login(String username) {

    if (username.isBlank()) {

        throw new InvalidLoginException(
            "Username cannot be empty."
        );

    }

}
```

No `throws` is required because this is an unchecked exception.

---

# Checked vs Unchecked Custom Exceptions

| Checked                     | Unchecked                                         |
| --------------------------- | ------------------------------------------------- |
| Extends `Exception`         | Extends `RuntimeException`                        |
| Must be handled or declared | Optional to handle                                |
| Usually recoverable         | Usually programming or business validation errors |
| Compiler enforces handling  | Compiler does not enforce handling                |

---

# Which One Should I Choose?

A common guideline is:

### Choose a Checked Exception

When the caller is expected to recover.

Example:

```text
InsufficientFundsException
```

The caller might:

* Ask the user for another amount.
* Cancel the withdrawal.
* Transfer money first.

---

### Choose an Unchecked Exception

When the caller has violated the API or provided invalid arguments.

Example:

```text
InvalidLoginException
```

or

```text
InvalidAgeException
```

if your design considers invalid ages to be programming mistakes rather than recoverable situations.

There is no universal rule. The correct choice depends on how you expect callers to respond.

---

# Designing Good Exception Messages

Poor message:

```text
Error.
```

Slightly better:

```text
Invalid age.
```

Professional:

```text
Student must be at least 18 years old.
```

Even better:

```text
Student age (16) is below the minimum allowed age of 18.
```

A good exception message should answer:

* What happened?
* Why did it happen?
* What value caused the problem (when useful)?

---

# Common Beginner Mistakes

## Mistake 1

Creating a custom exception for every small problem.

Not every validation deserves a new class.

Use existing Java exceptions when they already describe the problem well.

---

## Mistake 2

Extending `Error`.

Application-specific exceptions should almost always extend:

* `Exception`, or
* `RuntimeException`

Never `Error`.

---

## Mistake 3

Forgetting constructors.

A custom exception should usually provide at least a constructor that accepts a message.

---

## Mistake 4

Using generic names.

Bad:

```text
MyException
```

Good:

```text
InvalidAgeException
```

The name should clearly describe the failure.

---

# Professional Best Practices

* Group custom exceptions inside a dedicated `exception` package.
* Give exceptions descriptive names.
* Write meaningful messages.
* Prefer built-in exceptions when they already fit.
* Create custom exceptions only when they improve the clarity of your domain.
* Choose checked or unchecked exceptions intentionally based on how callers should respond.

---

# Guided Exercise 4 — Bank Account

Now we'll replace a generic exception with a domain-specific one.

---

## Step 1 — Project Structure

```text
src/
├── Main.java
├── model/
│   └── BankAccount.java
├── service/
│   └── BankService.java
└── exception/
    └── InsufficientFundsException.java
```

---

## Step 2 — Create `InsufficientFundsException`

```java
package exception;

public class InsufficientFundsException
        extends Exception {

    public InsufficientFundsException(String message) {

        super(message);

    }

}
```

---

## Step 3 — Create `BankAccount`

```java
package model;

public class BankAccount {

    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    public double getBalance() {
        return balance;
    }

    public void withdraw(double amount) {
        balance -= amount;
    }

}
```

---

## Step 4 — Create `BankService`

```java
package service;

import exception.InsufficientFundsException;
import model.BankAccount;

public class BankService {

    public void withdraw(
            BankAccount account,
            double amount)
            throws InsufficientFundsException {

        if (amount > account.getBalance()) {

            throw new InsufficientFundsException(
                "Withdrawal exceeds available balance."
            );

        }

        account.withdraw(amount);

        System.out.println("Withdrawal completed.");

    }

}
```

---

## Step 5 — Test in `Main`

```java
import exception.InsufficientFundsException;
import model.BankAccount;
import service.BankService;

public class Main {

    public static void main(String[] args) {

        BankService service = new BankService();

        BankAccount account = new BankAccount(200);

        try {

            service.withdraw(account, 500);

        } catch (InsufficientFundsException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

### Expected Output

```text
Withdrawal exceeds available balance.
```

### Experiments

Try different withdrawal amounts:

* `50`
* `200`
* `250`
* `500`

Observe:

* When is the exception thrown?
* When is the withdrawal successful?
* How does the custom exception make the code easier to understand?

---

# Chapter Summary

In this chapter, you learned that:

* Custom exceptions represent business-specific problems.
* They should be organized in a dedicated `exception` package.
* Checked custom exceptions extend `Exception`.
* Unchecked custom exceptions extend `RuntimeException`.
* Good exception names and messages make applications easier to understand and maintain.
* Custom exceptions integrate seamlessly with Java's existing exception handling system.

You now know how to design exceptions that accurately represent your application's domain instead of relying solely on generic Java exceptions.

---

# ✔️ Next Step

Proceed to **Chapter 11 — Java Built-in Exceptions**, where you'll study the most common exceptions you'll encounter in everyday Java development, learn what causes each one, how to reproduce them safely, how to prevent them, and the professional practices used to avoid them.
