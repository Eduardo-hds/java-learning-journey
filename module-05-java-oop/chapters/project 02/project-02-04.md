# 🏦 Project 2 — Stage 4: Deposits and Withdrawals Through the `BankManager`

At this point, your Bank System can:

* ✅ Create accounts
* ✅ Store multiple accounts
* ✅ Search for accounts
* ✅ Display all accounts

However, there is still one problem.

Right now, to deposit money, you must already have a reference to the `BankAccount` object.

Example:

```java
account.deposit(500);
```

But in a real banking system, the user usually knows only the **account number**, not the object reference.

This is where the `BankManager` becomes useful.

---

# 🎯 Stage Goal

Allow deposits and withdrawals using only the account number.

Example:

```java
manager.deposit("1001", 500);

manager.withdraw("1001", 200);
```

The manager will:

* Find the correct account
* Ask that account to perform the operation
* Return whether the operation succeeded

Notice something important:

The manager **does not** modify the balance directly.

The `BankAccount` still controls its own balance.

---

# 🧠 Why Doesn't `BankManager` Modify the Balance?

Imagine writing:

```java
account.balance += amount;
```

There are two problems:

1. `balance` is private.
2. This completely bypasses all validation.

Instead:

```java
account.deposit(amount);
```

The account decides whether the operation is allowed.

This is encapsulation in action.

---

# 🏗️ Step 1 — Create `deposit()`

Inside `BankManager`, create:

```java
public boolean deposit(String accountNumber, double amount)
```

The method should:

1. Search for the account.
2. If the account doesn't exist:

   * Return `false`.
3. Otherwise:

   * Call:

```java
account.deposit(amount);
```

4. Return the result.

Notice how short this method is.

Because the business logic already exists inside `BankAccount`.

---

# 🧠 Method Flow

Conceptually:

```text
Main

↓

BankManager.deposit()

↓

findAccount()

↓

BankAccount.deposit()

↓

Return result
```

Each class performs only its own responsibility.

---

# 🏗️ Step 2 — Create `withdraw()`

Now create:

```java
public boolean withdraw(String accountNumber, double amount)
```

The logic is almost identical.

Find the account.

If it doesn't exist:

```java
return false;
```

Otherwise:

```java
return account.withdraw(amount);
```

Again, the manager delegates the work to the account.

---

# 🧪 Testing Deposits

Create an account:

```java
BankAccount account =
    new BankAccount(
        "1001",
        "John",
        500
    );

manager.addAccount(account);
```

Deposit:

```java
boolean success =
    manager.deposit(
        "1001",
        300
    );
```

Expected balance:

```text
800
```

---

# 🧪 Testing Invalid Deposits

Deposit:

```java
manager.deposit("1001", -200);
```

Expected:

```text
Operation failed.
```

Balance remains:

```text
800
```

The account protected itself.

---

# 🧪 Testing Withdrawals

Withdraw:

```java
manager.withdraw(
    "1001",
    250
);
```

Balance:

```text
550
```

Calculation:

```text
800

-250

=

550
```

---

# 🧪 Testing Insufficient Funds

Attempt:

```java
manager.withdraw(
    "1001",
    5000
);
```

Expected:

```text
Operation failed.
```

Balance remains unchanged.

---

# 🧠 Internal Communication

When executing:

```java
manager.deposit("1001", 300);
```

Java performs something like:

```text
Main

↓

BankManager

↓

findAccount()

↓

BankAccount

↓

deposit()

↓

Balance updated

↓

Return true
```

Notice that no class accesses another object's private fields.

Everything happens through methods.

---

# 💡 Code Reuse

Notice how we reused an existing method.

Instead of rewriting deposit validation inside the manager:

```java
if (amount > 0)
```

we simply call:

```java
account.deposit(amount);
```

This avoids duplicated logic.

If deposit rules change in the future, only `BankAccount` needs to be updated.

---

# 🧠 Design Principle

The manager coordinates operations.

The account enforces business rules.

### BankManager

Responsible for:

* Finding accounts
* Coordinating operations

---

### BankAccount

Responsible for:

* Protecting the balance
* Validating deposits
* Validating withdrawals

Neither class takes over the other's responsibilities.

---

# 🏗️ Current Architecture

```text
               Main
                 │
                 ▼
          BankManager
        ├── findAccount()
        ├── deposit()
        └── withdraw()
                 │
                 ▼
          BankAccount
        ├── deposit()
        ├── withdraw()
        └── getBalance()
```

The manager acts as a bridge between the application and the accounts.

---

# 🚀 Looking Ahead

Now that deposits and withdrawals work through the manager, you're ready for a more advanced operation:

**Money transfers.**

A transfer is interesting because it involves **two different objects**:

* One account loses money.
* Another account receives money.

The manager will coordinate this interaction while each account continues enforcing its own rules.

This is one of the best examples of objects collaborating in Object-Oriented Programming.

---

# ✔️ Stage 4 Complete

Excellent!

Your Bank System now supports:

* ✅ Creating accounts
* ✅ Storing accounts
* ✅ Searching accounts
* ✅ Listing accounts
* ✅ Depositing money by account number
* ✅ Withdrawing money by account number

You have also reinforced one of the most important OOP principles: **objects should expose behavior through methods instead of allowing direct access to their internal state.**

## ▶️ Next Step

Continue to **Project 2 — Stage 5: Transferring Money Between Accounts**, where you'll implement the first operation involving communication between multiple objects, coordinating transfers safely while preserving encapsulation and business rules.
