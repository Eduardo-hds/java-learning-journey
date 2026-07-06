# 🏦 Project 2 — Stage 5: Transferring Money Between Accounts

So far, every banking operation has involved **only one account**.

Examples:

```text
Deposit

↓

One account
```

```text
Withdraw

↓

One account
```

Now we'll implement one of the most common banking operations:

**Money Transfer**

This operation is different because it involves **two different objects** interacting with each other.

---

# 🎯 Stage Goal

Implement a transfer feature that allows money to move safely from one account to another.

By the end of this stage, your application will be able to:

* Find the source account
* Find the destination account
* Withdraw money from the source account
* Deposit money into the destination account
* Prevent invalid transfers
* Keep both accounts consistent

---

# 🧠 Real-World Scenario

Imagine the following accounts:

```text
Account A

John

Balance: $1000
```

```text
Account B

Sarah

Balance: $300
```

John transfers:

```text
$250
```

After the transfer:

```text
John

$750
```

```text
Sarah

$550
```

Both accounts changed.

This means two different objects participated in a single operation.

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

Only `BankManager` will be updated.

---

# 🏗️ Step 1 — Create the Method

Inside `BankManager`, create:

```java
public boolean transfer(
    String fromAccount,
    String toAccount,
    double amount
)
```

Return:

* `true` if the transfer succeeds.
* `false` if any step fails.

---

# 🧠 Why Does the Transfer Belong in `BankManager`?

A common beginner question is:

> Why not put `transfer()` inside `BankAccount`?

Imagine this:

```java
account.transfer(otherAccount, 500);
```

It works.

But then every account would need to know about every other account.

Instead:

```text
Main

↓

BankManager

↓

Account A

↓

Account B
```

The manager coordinates the interaction.

The accounts remain independent.

---

# 🏗️ Step 2 — Find Both Accounts

Search for:

```java
BankAccount sender =
    findAccount(fromAccount);

BankAccount receiver =
    findAccount(toAccount);
```

If either account is `null`:

```java
return false;
```

The transfer cannot happen.

---

# 🏗️ Step 3 — Prevent Self-Transfers

Suppose someone writes:

```text
Transfer

From: 1001

To: 1001
```

This operation makes no sense.

Check:

```java
fromAccount.equals(toAccount)
```

If they are equal:

```java
return false;
```

This prevents unnecessary processing.

---

# 🏗️ Step 4 — Withdraw First

Never deposit money before withdrawing it.

Correct order:

```text
Withdraw

↓

Deposit
```

Attempt:

```java
sender.withdraw(amount);
```

If it returns:

```java
false
```

Stop immediately.

Do **not** deposit anything.

---

# 🧠 Why Withdraw First?

Imagine:

```text
John

Balance: $100
```

Transfer:

```text
$500
```

If we deposit first:

```text
Sarah

+500
```

Then discover John doesn't have enough money...

The bank would accidentally create money.

Always verify that the sender can pay before crediting the receiver.

---

# 🏗️ Step 5 — Deposit

If the withdrawal succeeds:

```java
receiver.deposit(amount);
```

Since the withdrawal already validated the amount and available balance, the deposit should succeed.

Finally:

```java
return true;
```

---

# 🧪 Testing

Create two accounts:

```java
BankAccount john =
    new BankAccount(
        "1001",
        "John",
        1000
    );

BankAccount sarah =
    new BankAccount(
        "1002",
        "Sarah",
        500
    );
```

Add them:

```java
manager.addAccount(john);
manager.addAccount(sarah);
```

Transfer:

```java
manager.transfer(
    "1001",
    "1002",
    300
);
```

Expected balances:

```text
John

700
```

```text
Sarah

800
```

---

# 🧪 Testing Invalid Cases

## Source Account Doesn't Exist

```java
manager.transfer(
    "9999",
    "1002",
    100
);
```

Expected:

```text
Transfer failed.
```

---

## Destination Account Doesn't Exist

```java
manager.transfer(
    "1001",
    "9999",
    100
);
```

Expected:

```text
Transfer failed.
```

---

## Insufficient Funds

John:

```text
Balance

100
```

Transfer:

```text
500
```

Expected:

```text
Transfer failed.
```

Balances remain unchanged.

---

## Same Account

```java
manager.transfer(
    "1001",
    "1001",
    100
);
```

Expected:

```text
Transfer failed.
```

---

# 🧠 Internal Execution

Conceptually:

```text
Main

↓

BankManager

↓

Find Sender

↓

Find Receiver

↓

Withdraw

↓

Deposit

↓

Return true
```

Notice that the manager **never** modifies balances directly.

It simply coordinates communication between objects.

---

# 💡 Object Collaboration

This is one of the clearest examples of Object-Oriented Programming.

Each object contributes part of the work.

```text
BankManager

↓

Coordinates
```

```text
BankAccount

↓

Protects balance
```

```text
BankAccount

↓

Receives deposit
```

Together they complete one business operation.

---

# 🧠 Design Principle

This stage demonstrates an important OOP idea:

> **Objects collaborate by sending messages (method calls) to each other.**

The manager doesn't say:

```text
Increase balance.
```

Instead, it asks:

```java
deposit(amount);
```

Likewise, it doesn't decrease balances directly.

It requests:

```java
withdraw(amount);
```

Every object remains responsible for its own internal state.

---

# 🏗️ Updated Project Architecture

```text
               Main
                 │
                 ▼
          BankManager
     ├── addAccount()
     ├── findAccount()
     ├── deposit()
     ├── withdraw()
     └── transfer()
          │         │
          ▼         ▼
     BankAccount  BankAccount
```

For the first time in this Bootcamp, you've built a feature where multiple objects work together to complete a single operation.

This pattern is used constantly in professional software.

---

# ✔️ Stage 5 Complete

Excellent!

Your Bank System now supports:

* ✅ Creating accounts
* ✅ Storing accounts
* ✅ Searching accounts
* ✅ Listing accounts
* ✅ Depositing money
* ✅ Withdrawing money
* ✅ Transferring money between accounts

You have also learned how to coordinate multiple objects while keeping each one responsible only for its own behavior—a fundamental concept in Object-Oriented Programming.

## ▶️ Next Step

Continue to **Project 2 — Stage 6: Final Polish and Refactoring**, where you'll improve code organization, eliminate duplication, review design decisions, and prepare the project as a clean, professional object-oriented application before moving on to the final project of this module.
