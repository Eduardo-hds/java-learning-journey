# 🚀 Module 02 — Final Project: Control Flow System (Console Java)

## 🎯 Objective

Build a **complete console-based Java system** that combines everything you learned in this module:

* Conditionals (`if`, `else`, `switch`)
* Loops (`while`, `do while`, `for`)
* Flow control (`break`, `continue`, `return`)

---

# 🧩 Project Overview

You will create a **single program** with a menu that contains 3 systems:

1. 🏧 ATM System (Caixa Eletrônico)
2. 🔐 Login System
3. 🎮 Guessing Game

The program runs in a loop until the user chooses to exit.

---

# 🧱 Base Structure Requirement

* Must use a main menu (`do while`)
* Must use `switch` to select options
* Must use loops inside each system
* Must use flow control (`break`, `continue`, `return`) appropriately

---

# 📋 Main Menu

Your program should start like this:

```
===== MAIN MENU =====
1 - ATM System
2 - Login System
3 - Guessing Game
0 - Exit
=====================
```

---

# 🏧 1. ATM System (Caixa Eletrônico)

## Features:

Inside this system, create another menu:

```
===== ATM MENU =====
1 - Check Balance
2 - Deposit
3 - Withdraw
0 - Back
====================
```

## Rules:

* Balance starts at `1000`
* Deposit adds to balance
* Withdraw subtracts from balance
* Cannot withdraw if insufficient funds
* Must return to main menu when selecting `0`

## Required concepts:

* `while` or `do while`
* `switch`
* `if / else`
* `break`

---

# 🔐 2. Login System

## Rules:

* Correct username: `admin`
* Correct password: `1234`
* User has **3 attempts**

## Behavior:

* If correct → show "Login successful"
* If wrong → decrease attempts
* After 3 failures → block access

## Required concepts:

* `while`
* `if / else`
* `break`
* `continue` (optional for retry logic)

---

# 🎮 3. Guessing Game

## Rules:

* Generate a number between 1 and 10
* User must guess the number
* Program gives hints:

  * "Too high"
  * "Too low"
* Stops when correct answer is found

## Required concepts:

* `while`
* `break`
* `if / else`
* `continue`

---

# ⚙️ Technical Requirements

Your solution must include:

* Only **console input/output**
* Only **basic Java syntax**
* No OOP (no classes beyond `main`)
* Proper loop control (no infinite loops)
* Clean and readable structure

---

# 🧠 What this project tests

You should demonstrate:

* Ability to control program flow
* Proper use of loops
* Correct use of `switch` menus
* Combining multiple systems in one program
* Logical thinking

---

# 🏁 Final Output Expectation

A single Java program that:

* Starts with a menu
* Lets user navigate between systems
* Runs each system independently
* Returns cleanly to main menu
* Exits only when user chooses
