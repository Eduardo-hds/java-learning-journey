# 🏦 Project 2 — Bank System

Welcome to your second project!

In the first project, you learned how to build a complete CRUD system using objects.

Now we'll take the next step.

This project focuses less on managing a collection of objects and more on **business logic**.

A bank account is a perfect example because it has rules that must always be respected.

For example:

* You cannot deposit a negative amount.
* You cannot withdraw more than your balance.
* Your balance should never become negative.

These rules make this project an excellent exercise for **encapsulation**.

---

# 🎯 Project Goal

Build a simple console-based Bank System capable of managing bank accounts and performing secure banking operations.

By the end of this project, the application will be able to:

* Create bank accounts
* Deposit money
* Withdraw money
* Display account information
* Transfer money between accounts
* List all accounts

Every operation must respect the business rules of a real bank.

---

# 📚 Concepts Practiced

This project reinforces:

* Object-Oriented Design
* Encapsulation
* Constructors
* Object communication
* Business rules
* Data validation
* Arrays
* Separation of responsibilities

---

# 📁 Project Structure

```text
src/
├── Main.java
├── model/
│   └── BankAccount.java
├── service/
│   └── BankManager.java
└── util/
```

Notice the similarity with Project 1.

Each class has a specific responsibility.

---

# 🧠 Responsibilities

## BankAccount

Represents **one bank account**.

Responsible for:

* Account number
* Owner
* Balance
* Deposit
* Withdraw
* Display account information

A `BankAccount` should **not** know about other accounts.

---

## BankManager

Responsible for:

* Storing accounts
* Creating accounts
* Searching accounts
* Listing accounts
* Transferring money

The manager coordinates the interaction between multiple accounts.

---

## Main

Responsible for:

* Starting the application
* Creating objects
* Calling methods
* Displaying results

---

# 🏗️ Project Development Roadmap

We'll build the project progressively.

## Stage 1

Project setup.

---

## Stage 2

Create the `BankAccount` class.

---

## Stage 3

Create the `BankManager`.

---

## Stage 4

Deposit money.

---

## Stage 5

Withdraw money.

---

## Stage 6

Transfer money between accounts.

---

## Stage 7

List all accounts.

---

## Stage 8

Final cleanup and refactoring.

---

# 🚀 Stage 1 — Project Setup

Create the following structure:

```text
src/
├── Main.java
├── model/
│   └── BankAccount.java
├── service/
│   └── BankManager.java
└── util/
```

Initially:

* `BankAccount.java` can be an empty class.
* `BankManager.java` can be an empty class.

Update `Main.java`:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("===== Bank System =====");

    }

}
```

Expected output:

```text
===== Bank System =====
```

---

# 💡 Why Build Another Manager?

Just like in Project 1:

One account should never manage every other account.

Imagine this:

```text
BankAccount

↓

createAccount()

deleteAccount()

transferMoney()

listAccounts()
```

That mixes two different responsibilities.

Instead:

```text
BankAccount

↓

Represents ONE account
```

```text
BankManager

↓

Manages MANY accounts
```

This keeps the design clean and scalable.

---

# 🧠 Real-World Mapping

Think of a real bank.

Each customer owns an account.

The account knows:

* Owner
* Balance
* Account number

But the account does **not** know:

* Every other customer
* Every other account

The bank itself manages all accounts.

Our project models this relationship.

---

# ✔️ Stage 1 Complete

Your project structure is now ready.

In the next stage, you'll build the `BankAccount` class with:

* Private attributes
* Constructors
* Encapsulation
* Deposit and withdrawal operations
* Validation rules
* A method to display account information

This class will become the foundation of the entire Bank System.

## ▶️ Next Step

Continue to **Project 2 — Stage 2: Building the `BankAccount` Class**, where you'll implement a fully encapsulated bank account that enforces real-world banking rules and protects its internal state.
