# 🏦 Project 2 — Stage 2: Building the `BankAccount` Class

Now that the project structure is ready, it's time to build the core of our banking system.

Every account in the system will be represented by a `BankAccount` object.

Just like the `Student` class represented a single student, the `BankAccount` class will represent **one and only one bank account**.

---

# 🎯 Stage Goal

By the end of this stage, the `BankAccount` class will:

* Store account information
* Protect its internal data
* Allow deposits
* Allow withdrawals
* Prevent invalid operations
* Display account information

---

# 📁 Project Structure

```text id="p2-stage2-structure"
src/
├── Main.java
├── model/
│   └── BankAccount.java
├── service/
│   └── BankManager.java
└── util/
```

Only `BankAccount.java` will be implemented in this stage.

---

# 🏗️ Step 1 — Define the Attributes

Create the following private attributes:

```java id="p2-stage2-fields"
private String accountNumber;
private String owner;
private double balance;
```

Each attribute has a specific purpose:

* `accountNumber` uniquely identifies the account.
* `owner` stores the account holder's name.
* `balance` stores the current amount of money.

Because these fields are `private`, they cannot be modified directly from outside the class.

---

# 🏗️ Step 2 — Create the Constructors

## Default Constructor

```java id="p2-default-constructor"
public BankAccount() {
    this("000000", "Unknown", 0.0);
}
```

---

## Parameterized Constructor

```java id="p2-parameterized-constructor"
public BankAccount(String accountNumber, String owner, double balance) {

    setAccountNumber(accountNumber);
    setOwner(owner);

    if (balance >= 0) {
        this.balance = balance;
    }

}
```

Notice something interesting.

For the initial balance, we assign it directly after validating it.

Why?

Because there is no deposit happening here.

We're simply creating the account.

Later, deposits will go through the `deposit()` method.

---

# 🧠 Why Doesn't the Constructor Call `deposit()`?

Imagine creating an account with:

```text
Initial Balance: 500
```

If the constructor called:

```java
deposit(500);
```

The program would print:

```text
Deposit successful.
```

But nobody actually deposited money.

The account simply started with an initial balance.

Initialization and business operations should remain separate.

---

# 🏗️ Step 3 — Create Getters

Create getters for:

* `accountNumber`
* `owner`
* `balance`

Example:

```java id="getter-example"
public String getOwner() {
    return owner;
}
```

Notice that `balance` has a getter but **no direct access**.

Other classes can read the balance but cannot change it directly.

---

# 🏗️ Step 4 — Create Setters

Create setters only where appropriate.

### Account Number

Validate:

* Cannot be `null`
* Cannot be blank

---

### Owner

Validate:

* Cannot be `null`
* Cannot be blank

---

### Balance

Should **not** have a public setter.

Why?

Imagine this:

```java
account.setBalance(1000000);
```

That completely bypasses the banking rules.

The balance should only change through:

* Deposit
* Withdraw
* Transfer (later)

This is a perfect example of encapsulation.

---

# 🏗️ Step 5 — Implement `deposit()`

Create:

```java id="deposit-signature"
public boolean deposit(double amount)
```

Rules:

* Amount must be greater than zero.
* If valid:

  * Increase the balance.
  * Return `true`.
* Otherwise:

  * Return `false`.

Conceptually:

```text
Current Balance

↓

+ Deposit

↓

New Balance
```

---

# 🧠 Why Return a Boolean?

Instead of printing:

```text
Deposit successful.
```

inside the method, return:

```java
true
```

Then `Main` decides what message should be shown.

This keeps the business logic independent from the user interface.

---

# 🏗️ Step 6 — Implement `withdraw()`

Create:

```java id="withdraw-signature"
public boolean withdraw(double amount)
```

Rules:

* Amount must be greater than zero.
* Balance must be sufficient.

If:

```text
Balance: 500

Withdraw: 200
```

Result:

```text
Balance: 300
```

If:

```text
Balance: 500

Withdraw: 800
```

Result:

The operation fails.

The balance remains unchanged.

---

# 🧠 Why Is This Validation Inside `BankAccount`?

Imagine someone writes:

```java
account.withdraw(1000000);
```

The object itself decides whether the operation is allowed.

Nobody outside the class can force the balance to become negative.

This is one of the strongest benefits of encapsulation.

---

# 🏗️ Step 7 — Create `displayAccountInformation()`

Add a method that prints:

```text
-----------------------------
Account Information
-----------------------------
Account Number: 1001
Owner         : John
Balance       : $500.00
-----------------------------
```

This formatting belongs inside the object.

---

# 🧪 Testing

Update `Main.java`.

Create an account:

```java
BankAccount account =
    new BankAccount(
        "1001",
        "John",
        500
    );
```

Display:

```java
account.displayAccountInformation();
```

Deposit:

```java
account.deposit(250);
```

Withdraw:

```java
account.withdraw(100);
```

Display again.

Expected balance:

```text
650
```

Calculation:

```text
500

+250

-100

=

650
```

---

# ⚠️ Common Beginner Mistakes

## Allowing Negative Deposits

Incorrect:

```java
balance += amount;
```

without validation.

Someone could call:

```java
deposit(-100);
```

which actually removes money.

---

## Allowing Negative Balance

Incorrect:

```java
balance -= amount;
```

without checking available funds.

Always verify the balance first.

---

## Public Balance Setter

Never do this:

```java
public void setBalance(double balance)
```

It completely breaks the banking rules.

---

# 🏗️ Current Architecture

```text
             Main
               │
               ▼
         BankAccount

        ├── deposit()
        ├── withdraw()
        ├── getBalance()
        └── displayAccountInformation()
```

At this point, there is only one account.

In the next stage, we'll introduce the manager that will coordinate multiple accounts.

---

# ✔️ Stage 2 Complete

Excellent!

You have built a fully encapsulated `BankAccount` class that models a real bank account instead of just storing data.

It now:

* Protects its internal state
* Validates deposits
* Prevents invalid withdrawals
* Exposes behavior through methods
* Keeps business rules inside the object where they belong

This is exactly how professional object-oriented software is designed.

## ▶️ Next Step

Continue to **Project 2 — Stage 3: Building the `BankManager` Class**, where you'll create the class responsible for managing multiple bank accounts, searching for accounts, and coordinating operations between them while keeping each `BankAccount` focused on representing a single account.
