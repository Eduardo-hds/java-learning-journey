# Chapter 15 — Final Project: Interactive Console Menu

Your banking system already has the core business logic.

Users can:

* Log in
* Deposit money
* Withdraw money

However, the application is still not interactive.

Everything is hardcoded inside `Main`.

A real console application allows the user to:

* type values,
* choose menu options,
* perform multiple operations,
* exit whenever they choose.

In this chapter, we'll connect everything you've built into a complete interactive application.

---

# Chapter Objectives

By the end of this chapter, you will:

* Create a console menu
* Read user input with `Scanner`
* Handle invalid menu choices
* Catch input errors gracefully
* Integrate the login and banking services
* Keep the application running until the user exits

---

# Updated Project Structure

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

No new packages are required.

We'll now integrate everything inside `Main`.

---

# Why Use a Menu Loop?

Imagine this application:

```text
Deposit

Program ends.
```

The user would need to restart the program for every operation.

Instead, we want:

```text
Login

↓

Menu

↓

Deposit

↓

Menu

↓

Withdraw

↓

Menu

↓

Balance

↓

Menu

↓

Exit
```

The menu should continue running until the user chooses to exit.

---

# Step 1 — Create the Scanner

```java
Scanner scanner = new Scanner(System.in);
```

We'll use it throughout the application to read user input.

Remember to import it:

```java
import java.util.Scanner;
```

---

# Step 2 — Perform Login

```java
System.out.print("Username: ");
String username = scanner.nextLine();

System.out.print("Password: ");
String password = scanner.nextLine();

User user = new User(username, password);

try {

    loginService.login(user);

} catch (InvalidLoginException e) {

    System.out.println(e.getMessage());

    scanner.close();
    return;

}
```

Notice that an invalid login ends the application.

Only authenticated users can access the banking menu.

---

# Step 3 — Create the Menu Loop

We'll use a `while` loop.

```java
boolean running = true;

while (running) {

    System.out.println();
    System.out.println("=== Banking Menu ===");
    System.out.println("1 - Deposit");
    System.out.println("2 - Withdraw");
    System.out.println("3 - Show Balance");
    System.out.println("0 - Exit");

    System.out.print("Choose an option: ");

}
```

The menu will repeat until the user chooses option `0`.

---

# Step 4 — Read the Menu Option Safely

Reading integers introduces a new possibility:

The user might type:

```text
abc
```

instead of:

```text
1
```

This throws:

```text
NumberFormatException
```

A safe approach is to read a line and convert it manually.

```java
int option;

try {

    option = Integer.parseInt(scanner.nextLine());

} catch (NumberFormatException e) {

    System.out.println("Please enter a valid menu option.");

    continue;

}
```

Notice the use of:

```java
continue;
```

The loop immediately restarts without terminating the application.

This provides a much better user experience.

---

# Step 5 — Process the Menu

```java
switch (option) {

    case 1:

        // Deposit

        break;

    case 2:

        // Withdraw

        break;

    case 3:

        // Balance

        break;

    case 0:

        running = false;

        break;

    default:

        System.out.println("Invalid option.");

}
```

This structure keeps the menu organized and easy to expand.

---

# Step 6 — Deposit Option

```java
case 1:

    try {

        System.out.print("Deposit amount: ");

        double amount =
                Double.parseDouble(scanner.nextLine());

        bankService.deposit(account, amount);

    } catch (NumberFormatException e) {

        System.out.println("Invalid number.");

    } catch (InvalidDepositException e) {

        System.out.println(e.getMessage());

    }

    break;
```

Notice that we handle two completely different problems:

* Invalid numeric input
* Invalid business rule

Each has its own `catch`.

---

# Step 7 — Withdrawal Option

```java
case 2:

    try {

        System.out.print("Withdrawal amount: ");

        double amount =
                Double.parseDouble(scanner.nextLine());

        bankService.withdraw(account, amount);

    } catch (NumberFormatException e) {

        System.out.println("Invalid number.");

    } catch (InsufficientFundsException e) {

        System.out.println(e.getMessage());

    }

    break;
```

Again, each exception has a clear responsibility.

---

# Step 8 — Balance Option

```java
case 3:

    System.out.println(
            "Current balance: $" +
            account.getBalance()
    );

    break;
```

This operation cannot fail under our current business rules, so no exception handling is needed.

---

# Step 9 — Exit

```java
case 0:

    running = false;

    System.out.println("Thank you for using the Banking System.");

    break;
```

The loop ends naturally.

---

# Step 10 — Close the Scanner

After the loop:

```java
scanner.close();
```

This releases the underlying input resource.

Although `System.in` is simple, closing resources is an excellent habit.

---

# Example Session

```text
Username: admin
Password: 1234

Login successful.

=== Banking Menu ===

1 - Deposit
2 - Withdraw
3 - Show Balance
0 - Exit

Choose an option: 1

Deposit amount: 200

Deposit completed successfully.

=== Banking Menu ===

Choose an option: 2

Withdrawal amount: 100

Withdrawal completed successfully.

=== Banking Menu ===

Choose an option: 3

Current balance: $600.0

=== Banking Menu ===

Choose an option: 0

Thank you for using the Banking System.
```

---

# Handling Invalid Input

Suppose the user enters:

```text
Deposit amount:

abc
```

Execution:

```text
Double.parseDouble()

↓

NumberFormatException

↓

catch

↓

Display error

↓

Return to menu
```

The application continues running.

This is exactly how professional console applications behave.

---

# Complete Application Flow

```text
Program Starts
        │
        ▼
Read Login
        │
        ▼
LoginService
        │
        ▼
Success?
   │         │
 No         Yes
 │           │
Exit      Menu Loop
             │
             ├───────────┐
             ▼           ▼
        Deposit     Withdraw
             │           │
             └─────┬─────┘
                   ▼
             Show Balance
                   │
                   ▼
             Continue?
              │       │
             Yes      No
              │       │
             Menu    Exit
```

---

# Common Beginner Mistakes

## Mistake 1

Using:

```java
scanner.nextInt();
```

instead of reading lines.

Mixing `nextInt()` and `nextLine()` often causes confusing input behavior.

Reading everything with:

```java
scanner.nextLine()
```

and converting manually is usually simpler.

---

## Mistake 2

Allowing one invalid input to terminate the application.

Recover whenever possible.

Return to the menu.

---

## Mistake 3

Duplicating validation in `Main`.

Keep business validation inside the service layer.

`Main` should coordinate the application, not enforce business rules.

---

## Mistake 4

Forgetting to close the scanner.

Always release resources when you're finished with them.

---

# Professional Best Practices

* Separate user interface from business logic.
* Read input safely.
* Catch exceptions at the appropriate level.
* Keep the application running after recoverable errors.
* Display meaningful messages to users.
* Keep menu code organized using `switch`.

---

# Final Project Progress

```text
Project Progress

██████████████████████□□ 90%

✔ Project structure
✔ Model classes
✔ Custom exceptions
✔ Login service
✔ Deposit service
✔ Withdrawal service
✔ Console menu
✔ User input
□ Final testing & polish
```

The banking system is now fully functional.

The only remaining step is to review, test, and polish the application to ensure it behaves correctly in every scenario.

---

# Chapter Summary

In this chapter, you:

* Built a complete interactive console menu.
* Integrated login, deposits, withdrawals, and balance checks.
* Safely handled invalid numeric input.
* Allowed the application to recover gracefully from recoverable errors.
* Connected all project components into a complete banking system.
* Applied nearly every exception-handling concept learned throughout this module.

Your project now behaves like a real console application.

---

# ✔️ Next Step

Proceed to **Chapter 16 — Final Project: Testing, Refactoring & Module Completion**, where you'll systematically test every feature, identify edge cases, perform small code improvements, review all concepts learned in Module 10, and generate the standardized **Module Completion Report** for the Bootcamp Central Control chat.
