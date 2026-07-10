# Chapter 13 — Final Project: Custom Exceptions & Login Service

Now that the project structure and model classes are ready, it's time to implement the **first piece of business logic**.

In this chapter, we'll build:

* The project's custom exceptions
* The authentication service
* The first real business validations
* Exception handling for login failures

This is the first time the application will actively enforce business rules instead of simply storing data.

---

# Chapter Objectives

By the end of this chapter, you will:

* Create the project's custom exceptions
* Organize them inside the `exception` package
* Implement the `LoginService`
* Validate user credentials
* Throw custom exceptions
* Handle login failures in `Main`
* Understand why authentication belongs in the service layer

---

# Step 1 — Create the Exception Package

Your project should now look like this:

```text
src/
│
├── Main.java
│
├── model/
│     ├── User.java
│     └── BankAccount.java
│
├── service/
│
├── exception/
│     ├── InvalidLoginException.java
│     ├── InvalidDepositException.java
│     └── InsufficientFundsException.java
│
└── util/
```

Although we'll only use one of these exceptions immediately, creating them now establishes the project's foundation.

---

# Step 2 — Create `InvalidLoginException`

Create:

```text
exception/
    InvalidLoginException.java
```

Implementation:

```java
package exception;

public class InvalidLoginException extends RuntimeException {

    public InvalidLoginException(String message) {
        super(message);
    }

}
```

Why extend `RuntimeException`?

Because invalid login credentials are considered invalid user input.

The compiler doesn't force callers to catch this exception, but our application will handle it to provide a better user experience.

---

# Step 3 — Create `InvalidDepositException`

```java
package exception;

public class InvalidDepositException extends Exception {

    public InvalidDepositException(String message) {
        super(message);
    }

}
```

Why is this checked?

Because the caller can recover by entering another deposit amount.

---

# Step 4 — Create `InsufficientFundsException`

```java
package exception;

public class InsufficientFundsException extends Exception {

    public InsufficientFundsException(String message) {
        super(message);
    }

}
```

Again, this is recoverable.

The user can:

* choose a smaller withdrawal,
* deposit more money,
* or cancel the operation.

---

# Exception Hierarchy

Our project now has the following hierarchy:

```text
Throwable
│
├── Exception
│     ├── InvalidDepositException
│     └── InsufficientFundsException
│
└── RuntimeException
      └── InvalidLoginException
```

This clearly separates checked and unchecked exceptions.

---

# Step 5 — Create `LoginService`

Create:

```text
service/
    LoginService.java
```

Implementation:

```java
package service;

import exception.InvalidLoginException;
import model.User;

public class LoginService {

    public void login(User user) {

        if (user == null) {
            throw new InvalidLoginException("User cannot be null.");
        }

        if (user.getUsername().isBlank()) {
            throw new InvalidLoginException("Username cannot be empty.");
        }

        if (user.getPassword().isBlank()) {
            throw new InvalidLoginException("Password cannot be empty.");
        }

        if (!user.getUsername().equals("admin")
                || !user.getPassword().equals("1234")) {

            throw new InvalidLoginException(
                    "Invalid username or password."
            );
        }

        System.out.println("Login successful.");

    }

}
```

---

# Why Validate in This Order?

Notice the sequence:

```text
Null check
        ↓
Username check
        ↓
Password check
        ↓
Credential validation
```

Each validation depends on the previous one.

For example:

Without this:

```java
if (user == null)
```

calling:

```java
user.getUsername()
```

would immediately throw a `NullPointerException`.

This is another example of **defensive programming**.

---

# Why Does `login()` Return `void`?

Some beginners expect something like:

```java
boolean login(User user)
```

That approach is valid in many applications.

However, for this module we intentionally use exceptions because the goal is to practice exception handling.

The method communicates failure by throwing an exception instead of returning `false`.

---

# Step 6 — Test in `Main`

```java
import exception.InvalidLoginException;
import model.BankAccount;
import model.User;
import service.LoginService;

public class Main {

    public static void main(String[] args) {

        User user = new User("admin", "1234");

        BankAccount account = new BankAccount(500);

        LoginService loginService = new LoginService();

        try {

            loginService.login(user);

            System.out.println("Current balance: $" +
                    account.getBalance());

        } catch (InvalidLoginException e) {

            System.out.println("Login failed.");

            System.out.println(e.getMessage());

        }

    }

}
```

---

# Expected Output

```text
Login successful.
Current balance: $500.0
```

---

# Experiment 1

Change:

```java
User user = new User("admin", "1234");
```

to:

```java
User user = new User("", "1234");
```

Output:

```text
Login failed.
Username cannot be empty.
```

---

# Experiment 2

Try:

```java
User user = new User("admin", "");
```

Output:

```text
Login failed.
Password cannot be empty.
```

---

# Experiment 3

Try:

```java
User user = new User("john", "password");
```

Output:

```text
Login failed.
Invalid username or password.
```

---

# Experiment 4

Try:

```java
User user = null;
```

Output:

```text
Login failed.
User cannot be null.
```

Notice how the `NullPointerException` never occurs because we validated the reference first.

---

# Execution Flow

Successful login:

```text
Main
 │
 ▼
login()
 │
 ▼
All validations pass
 │
 ▼
Login successful
 │
 ▼
Show balance
```

---

Failed login:

```text
Main
 │
 ▼
login()
 │
 ▼
Validation fails
 │
 ▼
throw InvalidLoginException
 │
 ▼
catch in Main
 │
 ▼
Display error message
```

This is the same exception flow you've been studying throughout the module.

---

# Common Beginner Mistakes

## Mistake 1

Validating credentials before checking for `null`.

Always validate object references first.

---

## Mistake 2

Returning `false` instead of throwing an exception when the exercise is specifically about exception handling.

---

## Mistake 3

Using vague messages such as:

```text
Login failed.
```

Instead, provide the reason whenever appropriate.

Examples:

* Username cannot be empty.
* Password cannot be empty.
* Invalid username or password.

---

## Mistake 4

Putting login validation inside the `User` class.

Remember:

```text
Model
↓

Stores data

Service
↓

Implements business rules
```

Keeping these responsibilities separate results in cleaner, more maintainable code.

---

# Professional Best Practices

* Validate object references before using them.
* Keep authentication logic inside the service layer.
* Throw descriptive exceptions for different failure scenarios.
* Use exception messages that help both users and developers understand the problem.
* Separate data models from business logic.

---

# Final Project Progress

```text
Project Progress

██████████████□□□□□□□□ 40%

✔ Project structure
✔ Model classes
✔ Custom exceptions
✔ Login service
□ Deposit service
□ Withdrawal service
□ Menu
□ Input validation
□ Final testing
```

The project is starting to become a real application.

Users can now authenticate, and invalid login attempts are handled gracefully using custom exceptions.

---

# Chapter Summary

In this chapter, you:

* Created three custom exception classes.
* Organized exceptions into a dedicated package.
* Built the `LoginService`.
* Implemented authentication using custom exceptions.
* Practiced defensive programming by validating object references before accessing them.
* Reinforced the separation of concerns between the model and service layers.

Your banking system can now authenticate users while handling login failures in a clean, maintainable way.

---

# ✔️ Next Step

Proceed to **Chapter 14 — Final Project: Deposit & Withdrawal Services**, where you'll implement the core banking operations, validate business rules using checked exceptions, and complete the main functionality of the banking system before adding the interactive console menu.
