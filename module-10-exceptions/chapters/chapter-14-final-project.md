# Chapter 14 — Final Project: Deposit & Withdrawal Services

The authentication system is now complete.

In this chapter, we'll implement the **core functionality** of the banking system:

* Deposits
* Withdrawals
* Business rule validation
* Checked custom exceptions
* Exception propagation

This chapter represents the heart of the application.

Every banking operation must guarantee that the account always remains in a valid state.

---

# Chapter Objectives

By the end of this chapter, you will:

* Implement deposits
* Implement withdrawals
* Validate deposit amounts
* Prevent overdrafts
* Throw checked custom exceptions
* Handle exceptions in `Main`
* Reinforce separation between model and service layers

---

# Current Project Structure

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
│     ├── LoginService.java
│     └── BankService.java
│
├── exception/
│     ├── InvalidLoginException.java
│     ├── InvalidDepositException.java
│     └── InsufficientFundsException.java
│
└── util/
```

Our focus is now the `BankService`.

---

# Why Use a Service?

You may wonder:

> "Why not put the validation inside `BankAccount`?"

For example:

```java
public void deposit(double amount) {

    if (amount <= 0) {
        ...
    }

}
```

Although this works, it mixes responsibilities.

Remember the architecture we've followed throughout the bootcamp:

```text
Model
    ↓
Stores data

Service
    ↓
Applies business rules
```

The model should represent the account.

The service should decide **whether an operation is allowed**.

---

# Step 1 — Implement Deposit

Open:

```text
service/
    BankService.java
```

Add the following method:

```java
package service;

import exception.InvalidDepositException;
import exception.InsufficientFundsException;
import model.BankAccount;

public class BankService {

    public void deposit(
            BankAccount account,
            double amount)
            throws InvalidDepositException {

        if (account == null) {

            throw new IllegalArgumentException(
                    "Account cannot be null."
            );

        }

        if (amount <= 0) {

            throw new InvalidDepositException(
                    "Deposit amount must be greater than zero."
            );

        }

        account.deposit(amount);

        System.out.println(
                "Deposit completed successfully."
        );

    }

}
```

---

# Why Check for `null`?

Notice this validation:

```java
if (account == null)
```

Without it:

```java
account.deposit(amount);
```

would produce a:

```text
NullPointerException
```

Instead of allowing Java to fail unexpectedly, we validate the argument ourselves.

This is defensive programming.

---

# Why Throw `IllegalArgumentException`?

The account reference is a **method argument**.

Passing `null` is considered invalid usage of the API.

Therefore:

```java
IllegalArgumentException
```

is an appropriate choice.

We reserve our custom exceptions for business rules.

---

# Step 2 — Implement Withdrawal

Add another method:

```java
public void withdraw(
        BankAccount account,
        double amount)
        throws InsufficientFundsException {

    if (account == null) {

        throw new IllegalArgumentException(
                "Account cannot be null."
        );

    }

    if (amount <= 0) {

        throw new IllegalArgumentException(
                "Withdrawal amount must be greater than zero."
        );

    }

    if (amount > account.getBalance()) {

        throw new InsufficientFundsException(
                "Insufficient balance."
        );

    }

    account.withdraw(amount);

    System.out.println(
            "Withdrawal completed successfully."
    );

}
```

---

# Business Rules

Deposit rules:

```text
Amount > 0
```

Withdrawal rules:

```text
Amount > 0

AND

Amount <= Balance
```

If either rule fails, the operation stops immediately.

---

# Execution Flow

Successful deposit:

```text
deposit()
      │
      ▼
Validate account
      ▼
Validate amount
      ▼
Deposit money
      ▼
Finish
```

Failed deposit:

```text
deposit()
      │
      ▼
Amount <= 0
      ▼
throw InvalidDepositException
      ▼
Caller handles exception
```

Successful withdrawal:

```text
withdraw()
      │
      ▼
Validate account
      ▼
Validate amount
      ▼
Check balance
      ▼
Withdraw
```

Failed withdrawal:

```text
withdraw()
      │
      ▼
Balance too low
      ▼
throw InsufficientFundsException
      ▼
Caller handles exception
```

---

# Step 3 — Test Deposits

Update `Main`.

```java
import exception.InvalidDepositException;
import exception.InsufficientFundsException;
import model.BankAccount;
import service.BankService;

public class Main {

    public static void main(String[] args) {

        BankAccount account = new BankAccount(500);

        BankService service = new BankService();

        try {

            service.deposit(account, 200);

            System.out.println(
                    "Balance: $" +
                    account.getBalance()
            );

        } catch (InvalidDepositException e) {

            System.out.println(e.getMessage());

        }

    }

}
```

Expected output:

```text
Deposit completed successfully.
Balance: $700.0
```

---

# Experiment

Try:

```java
service.deposit(account, -50);
```

Output:

```text
Deposit amount must be greater than zero.
```

---

# Step 4 — Test Withdrawals

Replace the previous test:

```java
try {

    service.withdraw(account, 300);

    System.out.println(
            "Balance: $" +
            account.getBalance()
    );

} catch (InsufficientFundsException e) {

    System.out.println(e.getMessage());

}
```

Output:

```text
Withdrawal completed successfully.
Balance: $200.0
```

---

# Experiment

Try:

```java
service.withdraw(account, 800);
```

Output:

```text
Insufficient balance.
```

Notice how the account balance never becomes negative.

The exception prevents an invalid state.

---

# Combining Multiple Operations

Now let's perform several operations in sequence.

```java
try {

    service.deposit(account, 100);

    service.withdraw(account, 50);

    service.withdraw(account, 1000);

} catch (InvalidDepositException e) {

    System.out.println(e.getMessage());

} catch (InsufficientFundsException e) {

    System.out.println(e.getMessage());

}

System.out.println(
        "Final balance: $" +
        account.getBalance()
);
```

Suppose the initial balance is:

```text
500
```

Execution:

1. Deposit 100 → Balance = 600
2. Withdraw 50 → Balance = 550
3. Withdraw 1000 → Exception

Final output:

```text
Deposit completed successfully.
Withdrawal completed successfully.
Insufficient balance.
Final balance: $550.0
```

The failed operation does not undo the successful ones that occurred before it.

---

# Why Are These Checked Exceptions?

Both:

* `InvalidDepositException`
* `InsufficientFundsException`

extend:

```java
Exception
```

This forces callers to acknowledge that these operations can fail.

The compiler helps ensure these situations are handled appropriately.

---

# Common Beginner Mistakes

## Mistake 1

Allowing negative balances.

Always validate before modifying the account.

---

## Mistake 2

Updating the balance before validation.

Incorrect:

```java
account.withdraw(amount);

if (...)
```

Validate first.

Modify later.

---

## Mistake 3

Duplicating validation inside the model.

Keep validation inside the service layer.

---

## Mistake 4

Throwing generic exceptions.

Instead of:

```java
throw new Exception("Error");
```

Use:

* `InvalidDepositException`
* `InsufficientFundsException`

These clearly communicate the business problem.

---

# Professional Best Practices

* Validate every public method argument.
* Reject invalid operations before modifying data.
* Keep models simple.
* Place business rules in services.
* Use custom exceptions to express domain-specific failures.
* Ensure objects remain in a valid state after exceptions.

---

# Final Project Progress

```text
Project Progress

██████████████████□□□□ 60%

✔ Project structure
✔ Model classes
✔ Custom exceptions
✔ Login service
✔ Deposit service
✔ Withdrawal service
□ Console menu
□ User input
□ Final testing
```

At this point, the banking logic is complete.

The remaining work is making the application interactive.

---

# Chapter Summary

In this chapter, you:

* Implemented deposit and withdrawal operations.
* Validated business rules before modifying data.
* Used checked custom exceptions to report recoverable failures.
* Prevented invalid account states such as negative balances.
* Reinforced the separation between the model and service layers.
* Practiced exception handling with multiple banking operations.

Your banking system now supports the essential banking features with robust validation and exception handling.

---

# ✔️ Next Step

Proceed to **Chapter 15 — Final Project: Interactive Console Menu**, where you'll build the user interface using `Scanner`, create a menu loop, safely handle invalid user input, integrate the login and banking services, and bring the entire application together into a complete console-based banking system.
