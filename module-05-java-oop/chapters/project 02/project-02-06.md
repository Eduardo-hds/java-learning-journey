# 🏦 Project 2 — Stage 6: Final Polish and Refactoring

Congratulations!

Your Bank System is now **feature complete**.

It supports:

* ✅ Creating accounts
* ✅ Storing multiple accounts
* ✅ Searching accounts
* ✅ Listing accounts
* ✅ Depositing money
* ✅ Withdrawing money
* ✅ Transferring money

Before moving to the final project, professional developers don't immediately start something new.

Instead, they review and improve the code they've written.

This process is called **refactoring**.

---

# 🎯 Stage Goal

Improve the quality of the project without changing its behavior.

By the end of this stage, you'll have:

* Cleaner code
* Better organization
* Less duplication
* More readable methods
* Better separation of responsibilities

The application should behave exactly the same—it will simply be easier to maintain.

---

# 🧠 What Is Refactoring?

Refactoring means:

> Improving the internal structure of the code **without changing what the program does**.

Example:

Before:

```java
if (account != null) {

    if (amount > 0) {

        if (account.withdraw(amount)) {

            return true;

        }

    }

}

return false;
```

After:

```java
if (account == null) {
    return false;
}

return account.withdraw(amount);
```

Both versions produce the same result.

The second one is much easier to read.

---

# 🏗️ Step 1 — Review Responsibilities

Check each class.

---

## Main

Should only:

* Create objects
* Call methods
* Display results

It should **not** contain banking rules.

---

## BankManager

Should only:

* Manage accounts
* Coordinate operations

It should **not** modify balances directly.

---

## BankAccount

Should:

* Protect its balance
* Validate operations
* Store account information

It should **not** manage other accounts.

---

# 🏗️ Step 2 — Remove Duplicate Code

Look through your methods.

Ask yourself:

> "Am I writing the same logic twice?"

Example:

Searching for an account should always use:

```java
findAccount(accountNumber)
```

Never rewrite the search loop in multiple methods.

Good software reuses existing methods whenever possible.

---

# 🏗️ Step 3 — Improve Method Names

Good method names explain exactly what they do.

Examples:

✅ Good

```java
deposit()
withdraw()
findAccount()
displayAccountInformation()
transfer()
```

Avoid vague names like:

```java
doSomething()
execute()
run()
process()
```

Your code should read almost like English.

---

# 🏗️ Step 4 — Review Validation

Check every public method.

Ask:

> "Can someone pass invalid data?"

Examples:

Deposit:

```text
Amount > 0
```

Withdraw:

```text
Amount > 0

Balance is sufficient
```

Transfer:

```text
Different accounts

Accounts exist

Amount > 0
```

Owner:

```text
Cannot be blank
```

Validation should always happen **before** changing an object's state.

---

# 🏗️ Step 5 — Review Encapsulation

Ask yourself:

Can another class directly modify the balance?

It should not.

Good:

```java
private double balance;
```

Bad:

```java
public double balance;
```

The only way to change the balance should be:

```java
deposit()

withdraw()
```

This guarantees that every balance change follows the banking rules.

---

# 🏗️ Step 6 — Test Edge Cases

Professional developers don't only test happy paths.

Try unusual situations.

### Deposit Zero

```java
manager.deposit("1001", 0);
```

Should fail.

---

### Withdraw Zero

```java
manager.withdraw("1001", 0);
```

Should fail.

---

### Negative Deposit

```java
manager.deposit("1001", -50);
```

Should fail.

---

### Transfer More Than Balance

Should fail.

---

### Search Non-Existent Account

Should return:

```java
null
```

---

### Empty Bank

Calling:

```java
manager.listAccounts();
```

Should print:

```text
No accounts registered.
```

Testing edge cases helps reveal bugs before users do.

---

# 🧠 Design Review

Look at your final architecture.

```text
               Main
                 │
                 ▼
          BankManager
     ├── addAccount()
     ├── findAccount()
     ├── deposit()
     ├── withdraw()
     ├── transfer()
     └── listAccounts()
                 │
      ┌──────────┴──────────┐
      ▼                     ▼
 BankAccount         BankAccount
```

Notice something important.

Every class has a very clear job.

This makes future improvements much easier.

---

# 💡 What You've Practiced

During this project, you reinforced almost every concept introduced in Module 05:

* Creating classes
* Instantiating objects
* Constructors
* Encapsulation
* Getters and setters
* Business rules
* Arrays
* Searching
* CRUD-style operations
* Object collaboration
* Package organization
* Clean architecture
* Refactoring

This is a strong foundation for larger Java applications.

---

# 🚀 Looking Ahead

Your final project will combine ideas from both previous projects.

Instead of focusing on one specific domain, you'll design a larger application with multiple classes interacting together.

You'll be responsible for thinking about:

* Which classes should exist
* What each class should do
* How objects communicate
* How to keep responsibilities separate

This is where you'll start thinking more like a software designer than just a programmer.

---

# ✔️ Project 2 Complete 🎉

Outstanding work!

You have successfully built a complete Bank System using Object-Oriented Programming principles.

More importantly, you've learned that professional software is not just about making code work—it's about organizing code so that it remains understandable, reusable, and easy to maintain.

Your project now demonstrates clean separation of responsibilities, proper encapsulation, and effective collaboration between objects.

## ▶️ Next Step

Continue to **Project 3 — Inventory Management System**, the final project of Module 05, where you'll combine everything you've learned throughout this module to build your most complete object-oriented application yet.
