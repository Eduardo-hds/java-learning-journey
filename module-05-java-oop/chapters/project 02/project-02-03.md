# 🏦 Project 2 — Stage 3: Building the `BankManager` Class

Our `BankAccount` class is now complete.

It can:

* ✅ Store account information
* ✅ Deposit money
* ✅ Withdraw money
* ✅ Protect its own data

However, a real banking system doesn't manage just one account.

It manages thousands—or even millions—of accounts.

That's why we need a new class:

**`BankManager`**

Its responsibility is to manage the collection of accounts, while each `BankAccount` remains responsible only for itself.

---

# 🎯 Stage Goal

By the end of this stage, your application will be able to:

* Store multiple bank accounts
* Add new accounts
* Search for an account by account number
* List all registered accounts

---

# 📁 Project Structure

```text id="p2-stage3-structure"
src/
├── Main.java
├── model/
│   └── BankAccount.java
├── service/
│   └── BankManager.java
└── util/
```

In this stage, we'll implement `BankManager.java`.

---

# 🧠 Why Do We Need a Manager?

Think about a real bank.

A bank account knows things like:

* Account number
* Owner
* Balance

But it **doesn't know**:

* Every other account in the bank
* How many accounts exist
* How to search through all accounts

Those responsibilities belong to the bank itself.

Our `BankManager` plays the role of the bank.

---

# 🏗️ Step 1 — Create the Attributes

Just like in Project 1, we'll use an array.

```java
private BankAccount[] accounts;
private int accountCount;
```

### What do these fields represent?

* `accounts` stores all registered accounts.
* `accountCount` tracks how many positions are actually in use.

Initially:

```text
accounts

↓

[ null, null, null, ..., null ]
```

After creating one account:

```text
accounts

↓

[ John, null, null, ..., null ]
```

`accountCount`

```text
1
```

---

# 🏗️ Step 2 — Create the Constructor

Initialize the array.

```java
public BankManager() {
    accounts = new BankAccount[100];
    accountCount = 0;
}
```

For this project, we'll allow a maximum of **100 accounts**.

---

# 🏗️ Step 3 — Implement `addAccount()`

Create:

```java
public boolean addAccount(BankAccount account)
```

Responsibilities:

* Verify that there is space.
* Add the account.
* Increase `accountCount`.
* Return `true`.

If the array is full:

Return:

```java
false
```

Notice that the manager is **not creating** the account.

It simply stores an already existing object.

---

# 🧠 Object Ownership

The flow looks like this:

```text
Main

↓

Creates BankAccount

↓

Passes it to BankManager

↓

BankManager stores it
```

The manager owns the collection.

The account owns its own data.

---

# 🏗️ Step 4 — Implement `findAccount()`

Create:

```java
public BankAccount findAccount(String accountNumber)
```

Search only until:

```java
accountCount
```

For each account:

```java
account.getAccountNumber().equals(accountNumber)
```

If found:

```java
return account;
```

Otherwise:

```java
return null;
```

---

# 🧠 Why Search by Account Number?

Could we search by owner?

Yes.

But imagine this:

```text
John Smith

John Smith

John Smith
```

Which account should we return?

The account number is unique.

That's why banks use it as the primary identifier.

---

# 🏗️ Step 5 — Implement `listAccounts()`

Create:

```java
public void listAccounts()
```

If there are no accounts:

```text
No accounts registered.
```

Otherwise:

Loop from:

```java
0
```

to:

```java
accountCount - 1
```

For each account:

```java
account.displayAccountInformation();
```

Again, the manager doesn't print the details itself.

It asks each account to display its own information.

---

# 🧪 Testing

Update `Main.java`.

Create three accounts.

Example:

```java
BankAccount account1 =
    new BankAccount(
        "1001",
        "John",
        500
    );

BankAccount account2 =
    new BankAccount(
        "1002",
        "Sarah",
        1200
    );

BankAccount account3 =
    new BankAccount(
        "1003",
        "Michael",
        800
    );
```

Add them:

```java
manager.addAccount(account1);
manager.addAccount(account2);
manager.addAccount(account3);
```

List them:

```java
manager.listAccounts();
```

Expected output:

```text
-----------------------------
Account Information
-----------------------------
Account Number: 1001
Owner         : John
Balance       : $500.00
-----------------------------

-----------------------------
Account Information
-----------------------------
Account Number: 1002
Owner         : Sarah
Balance       : $1200.00
-----------------------------

-----------------------------
Account Information
-----------------------------
Account Number: 1003
Owner         : Michael
Balance       : $800.00
-----------------------------
```

---

# 🧪 Testing the Search

Search for:

```java
BankAccount account =
    manager.findAccount("1002");
```

If found:

```java
account.displayAccountInformation();
```

Expected:

```text
Owner: Sarah
```

Search for:

```text
9999
```

Expected:

```text
Account not found.
```

---

# 🧠 Internal Execution

When searching for account **1002**, Java performs something like:

```text
1001

↓

Not a match

↓

1002

↓

Match found

↓

Return account

↓

Search ends
```

The search stops as soon as the correct account is found.

---

# 💡 Design Principle

Notice how responsibilities remain well organized.

### BankAccount

Responsible for:

* Representing one account
* Protecting the balance
* Performing deposits
* Performing withdrawals

---

### BankManager

Responsible for:

* Managing multiple accounts
* Adding accounts
* Searching accounts
* Listing accounts

---

### Main

Responsible for:

* Creating objects
* Calling manager methods
* Displaying results

No class is doing another class's job.

---

# 🏗️ Current Project Architecture

```text
               Main
                 │
                 ▼
          BankManager
      ├── addAccount()
      ├── findAccount()
      └── listAccounts()
                 │
        ┌────────┴────────┐
        ▼                 ▼
 BankAccount       BankAccount
```

This is a scalable architecture.

If tomorrow the bank has **10,000 accounts**, the responsibilities remain exactly the same.

---

# ✔️ Stage 3 Complete

Excellent!

Your Bank System can now:

* ✅ Create bank accounts
* ✅ Store multiple accounts
* ✅ Search accounts by account number
* ✅ Display every registered account

The project now has a solid object-oriented architecture, making it easy to extend with more advanced banking operations.

## ▶️ Next Step

Continue to **Project 2 — Stage 4: Deposits and Withdrawals Through the `BankManager`**, where you'll connect the manager with the `BankAccount` objects, allowing users to perform banking operations by account number while keeping all business rules safely encapsulated inside each account.
