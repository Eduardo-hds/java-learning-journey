# Chapter 8 — Final Project Implementation (Step-by-Step Build)

---

Now we move from **design → real implementation**.

We will build ONE system together, step by step, using proper abstraction.

I’ll choose a balanced option for learning:

> 🏦 **Banking System (best for abstract class understanding)**

---

# 🧠 1. Project Overview

We will build:

### Abstract Class:

* `Account`

### Concrete Classes:

* `SavingsAccount`
* `CheckingAccount`
* `BusinessAccount`
* `PremiumAccount`

---

# 📦 2. Package Structure

```text id="pkg_bank_01"
src/
 ├── Main.java
 ├── model/
 │    ├── Account.java
 │    ├── SavingsAccount.java
 │    ├── CheckingAccount.java
 │    ├── BusinessAccount.java
 │    └── PremiumAccount.java
```

---

# 🧩 3. Step 1 — Abstract Class (Core Design)

We start with the **base abstraction**.

### Think:

All accounts:

* have balance
* can deposit (shared behavior)
* must withdraw (rules differ)

---

## 🏗️ Account.java

```java id="acc_001"
package model;

abstract class Account {

    protected double balance;

    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount);
    }

    public double getBalance() {
        return balance;
    }

    public abstract void withdraw(double amount);
}
```

---

# 🧠 What you just learned:

✔ Shared logic → deposit()
✔ Shared state → balance
✔ Forced behavior → withdraw()

---

# 🧩 4. Step 2 — SavingsAccount

### Rule:

* Cannot withdraw if balance gets too low

---

## 🏗️ SavingsAccount.java

```java id="sav_001"
package model;

class SavingsAccount extends Account {

    @Override
    public void withdraw(double amount) {
        if (balance - amount < 100) {
            System.out.println("Withdrawal denied: minimum balance required");
        } else {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        }
    }
}
```

---

# 🧩 5. Step 3 — CheckingAccount

### Rule:

* Free withdrawals (simple behavior)

```java id="chk_001"
package model;

class CheckingAccount extends Account {

    @Override
    public void withdraw(double amount) {
        balance -= amount;
        System.out.println("Withdrawn: " + amount);
    }
}
```

---

# 🧩 6. Step 4 — BusinessAccount

### Rule:

* Has fee per withdrawal

```java id="bus_001"
package model;

class BusinessAccount extends Account {

    @Override
    public void withdraw(double amount) {
        double fee = 5.0;
        balance -= (amount + fee);
        System.out.println("Withdrawn: " + amount + " + fee: " + fee);
    }
}
```

---

# 🧩 7. Step 5 — PremiumAccount

### Rule:

* No restrictions, but bonus reward logic (simple simulation)

```java id="pre_001"
package model;

class PremiumAccount extends Account {

    @Override
    public void withdraw(double amount) {
        balance -= amount;
        System.out.println("Premium withdrawal: " + amount);
    }

    public void addBonus(double bonus) {
        balance += bonus;
        System.out.println("Bonus added: " + bonus);
    }
}
```

---

# 🧪 8. Step 6 — Main Class (Testing)

```java id="main_001"
import model.*;

public class Main {
    public static void main(String[] args) {

        Account savings = new SavingsAccount();
        Account checking = new CheckingAccount();
        Account business = new BusinessAccount();
        PremiumAccount premium = new PremiumAccount();

        savings.deposit(500);
        savings.withdraw(350);

        checking.deposit(1000);
        checking.withdraw(200);

        business.deposit(2000);
        business.withdraw(500);

        premium.deposit(3000);
        premium.withdraw(1000);
        premium.addBonus(200);

        System.out.println("Premium balance: " + premium.getBalance());
    }
}
```

---

# 🔥 9. What You Just Built (VERY IMPORTANT)

You implemented:

### ✔ Abstract Class

* shared structure
* enforced rule (withdraw)

### ✔ Inheritance

* multiple account types

### ✔ Polymorphism (implicit preview)

* Account reference used for different objects

### ✔ Real-world modeling

* banking logic separation

---

# 🧠 10. Key Learning Outcome

You now understand:

* How abstract classes define system rules
* How subclasses specialize behavior
* How shared logic reduces duplication
* How real systems are structured in Java

---

# 🚫 11. Common Mistakes to Avoid

❌ Putting withdraw logic in Account
❌ Not using abstract method properly
❌ Mixing unrelated rules in same class
❌ Ignoring inheritance hierarchy

---

# ✔️ Final Check

You should now be able to answer:

1. Why is Account abstract?
2. Why is withdraw abstract?
3. Why is deposit NOT abstract?
4. Why do subclasses behave differently?
5. What is shared vs what is customized?

---

# 🎉 Module 08 Completed

You have now learned:

* Abstract classes fundamentals
* Abstract methods
* Partial abstraction
* Inheritance with abstraction
* Design decisions
* Real system implementation

