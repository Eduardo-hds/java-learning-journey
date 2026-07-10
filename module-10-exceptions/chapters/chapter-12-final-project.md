# Chapter 12 — Final Project: Banking System with Exception Handling

Welcome to the final project of Module 10.

This project is designed to bring together **everything you've learned** throughout the module by building a realistic console-based banking application.

Unlike earlier exercises, this project will be developed **progressively**, just as software is built in professional environments.

We will **not** write the entire application at once. Instead, we'll add one feature at a time, test it, and then continue.

This approach helps you understand how different parts of the system interact and makes debugging much easier.

---

# Project Objectives

By the end of this project, you will have built a banking application that demonstrates:

* Proper package organization
* Object-Oriented Programming
* Exception handling
* Custom exceptions
* Exception propagation
* Defensive programming
* Business rule validation
* Clean code organization

---

# Features

The application will support:

* Create a bank account
* Deposit money
* Withdraw money
* Check account balance
* User login
* Validation of business rules
* Graceful error handling
* Console interaction

---

# Concepts Applied

During this project, you'll use:

* `try`
* `catch`
* `finally`
* `throw`
* `throws`
* Custom checked exceptions
* Custom unchecked exceptions
* Exception propagation
* Input validation
* Guard clauses
* Package organization

---

# Final Project Structure

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

Notice how each package has a clear responsibility.

---

# Package Responsibilities

## `model`

Contains application data.

Example:

```text
User
BankAccount
```

These classes represent the application's entities.

---

## `service`

Contains business logic.

Examples:

* login validation
* deposits
* withdrawals

Services decide **what the application does**.

---

## `exception`

Contains custom exceptions.

Examples:

```text
InvalidLoginException
InsufficientFundsException
InvalidDepositException
```

Keeping these classes together improves organization and scalability.

---

## `util`

Reserved for utility classes if needed.

This project will use it minimally, but keeping the package aligns with the project structure you've learned throughout the bootcamp.

---

# Business Rules

Our application will enforce the following rules:

### Login

* Username cannot be empty.
* Password cannot be empty.
* Invalid credentials produce an exception.

---

### Deposits

* Deposit must be greater than zero.

---

### Withdrawals

* Withdrawal must be greater than zero.
* Withdrawal cannot exceed the account balance.

---

### Balance

Balance can never become negative.

---

# Exception Design

We'll use three custom exceptions.

---

## `InvalidLoginException`

```text
extends RuntimeException
```

Reason:

An invalid login is considered invalid input from the caller.

---

## `InvalidDepositException`

```text
extends Exception
```

Reason:

The caller can recover by entering another amount.

---

## `InsufficientFundsException`

```text
extends Exception
```

Reason:

The caller can choose a different withdrawal amount or deposit more money.

---

# Execution Flow

The application flow will look like this:

```text
Application Starts
        │
        ▼
User Login
        │
        ▼
Main Menu
        │
        ├──────────────┐
        ▼              ▼
 Deposit        Withdraw
        │              │
        └──────┬───────┘
               ▼
        Show Balance
               ▼
        Continue / Exit
```

At every step, invalid operations will be handled through exceptions.

---

# Development Plan

Instead of writing everything at once, we'll build the project in small milestones.

## Milestone 1

Create the project structure.

---

## Milestone 2

Create model classes.

---

## Milestone 3

Create custom exceptions.

---

## Milestone 4

Implement login validation.

---

## Milestone 5

Implement deposits.

---

## Milestone 6

Implement withdrawals.

---

## Milestone 7

Create the menu.

---

## Milestone 8

Handle invalid user input.

---

## Milestone 9

Improve messages and validation.

---

## Milestone 10

Final testing and cleanup.

---

# Milestone 1 — Create the Project Structure

Create the following folders:

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
│
└── util/
```

Do **not** write any logic yet.

A well-organized project is easier to understand before adding functionality.

---

# Milestone 2 — Create the Model Classes

## `User`

```java
package model;

public class User {

    private String username;
    private String password;

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

}
```

---

## `BankAccount`

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

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        balance -= amount;
    }

}
```

Notice that these classes contain **data**, not business rules.

Validation will belong in the service layer.

---

# Why Keep Validation Out of the Model?

A beginner might write:

```java
public void deposit(double amount) {

    if (amount <= 0) {
        ...
    }

}
```

We'll avoid this for now.

Instead:

```text
Service
      ↓
Validates
      ↓
Model
      ↓
Stores data
```

This separation of responsibilities makes the application easier to maintain and test.

---

# Test the Project

Before adding services, verify that:

* The project compiles.
* Packages are correctly organized.
* Classes are in the proper directories.
* Constructors and getters work correctly.

Building incrementally helps catch problems early instead of after hundreds of lines of code.

---

# What We'll Build Next

In the next chapter, we'll begin implementing the **service layer**, starting with authentication and custom exceptions.

This is where the application starts enforcing business rules using everything you've learned in this module.

---

# Final Project Progress

```text
Project Progress

██████████□□□□□□□□□□□□ 20%

✔ Project structure
✔ Model classes
□ Custom exceptions
□ Login service
□ Deposit
□ Withdraw
□ Menu
□ Input validation
□ Final testing
```

---

# Chapter Summary

In this chapter, you:

* Defined the architecture of the final project.
* Created a professional package structure.
* Built the model layer.
* Established the project's business rules.
* Planned the development milestones.
* Reinforced the separation between data and business logic.

The foundation is now ready.

The next chapters will progressively transform this structure into a complete banking application with robust exception handling.

---

# ✔️ Next Step

Proceed to **Chapter 13 — Final Project: Custom Exceptions & Login Service**, where you'll implement the `exception` package, create the project's custom exceptions, and build the first business service responsible for authenticating users and handling invalid login attempts.
