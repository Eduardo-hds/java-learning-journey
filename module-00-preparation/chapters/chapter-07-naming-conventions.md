# Chapter 7 — Official Naming Conventions

## Overview

Writing code that works is only part of being a professional developer. Writing code that is easy to read, understand, and maintain is equally important.

Java has well-established naming conventions that are followed by developers and organizations around the world. These conventions improve readability, reduce confusion, and make collaboration easier.

In this chapter, we will learn the official Java naming conventions for packages, classes, interfaces, methods, variables, constants, and files.

---

## Objectives

By the end of this chapter, I will understand:

- Why naming conventions are important
- The official Java naming standards
- How to name packages correctly
- How to name classes and interfaces
- How to name methods and variables
- How to name constants
- Common naming mistakes to avoid

---

## Why Naming Conventions Matter

Naming conventions exist to create consistency across projects.

When every developer follows the same standards:

- Code becomes easier to read.
- Teams collaborate more efficiently.
- Maintenance becomes simpler.
- Projects become more professional.
- New developers can understand the codebase more quickly.

Readable code is just as important as functional code.

---

## Package Naming

Package names should always:

- Use only lowercase letters.
- Avoid special characters.
- Be descriptive.
- Follow the reversed domain convention whenever possible.

Good examples:

```text
com.company.project
```

```text
org.springframework.boot
```

```text
com.eduardohenrique.javabootcamp
```

Bad examples:

```text
Com.Project
```

```text
MyPackage
```

```text
Java_Project
```

---

## Class Naming

Class names use **PascalCase**.

Rules:

- Every word starts with a capital letter.
- Use nouns.
- Choose meaningful names.

Good examples:

```text
Customer
```

```text
BankAccount
```

```text
ProductService
```

Bad examples:

```text
customer
```

```text
bank_account
```

```text
myclass
```

---

## Interface Naming

Interfaces follow the same convention as classes.

Examples:

```text
Runnable
```

```text
Comparable
```

```text
PaymentService
```

Some projects prefix interfaces with `I`, but this is **not** the official Java convention.

Preferred:

```text
PaymentService
```

Avoid:

```text
IPaymentService
```

---

## Method Naming

Method names use **camelCase**.

Rules:

- First word starts with a lowercase letter.
- Each additional word starts with an uppercase letter.
- Methods should describe an action.

Good examples:

```text
calculateTotal()
```

```text
findCustomer()
```

```text
saveProduct()
```

Bad examples:

```text
CalculateTotal()
```

```text
calculate_total()
```

```text
method1()
```

---

## Variable Naming

Variables also use **camelCase**.

Examples:

```text
firstName
```

```text
accountBalance
```

```text
studentAge
```

Good variable names clearly describe the stored value.

Avoid abbreviations unless they are universally understood.

---

## Constant Naming

Constants use **UPPER_SNAKE_CASE**.

Rules:

- All letters uppercase.
- Words separated by underscores.

Examples:

```text
MAX_SIZE
```

```text
DEFAULT_TIMEOUT
```

```text
PI
```

This immediately identifies values that should never change.

---

## File Naming

Java files must have the same name as their public class.

Correct:

```text
Customer.java
```

Inside:

```java
public class Customer {
}
```

Incorrect:

```text
Customer.java
```

```java
public class Person {
}
```

The compiler will generate an error because the file name and public class name do not match.

---

## Boolean Naming

Boolean variables should clearly express a true or false condition.

Good examples:

```text
isActive
```

```text
hasPermission
```

```text
canLogin
```

These names make conditions easier to read.

Example:

```java
if (isActive) {
    ...
}
```

---

## Avoid Abbreviations

Prefer descriptive names over short abbreviations.

Good:

```text
customerAddress
```

Instead of:

```text
custAddr
```

Readable code is more valuable than short code.

---

## Common Mistakes

Avoid:

- Using uppercase letters in package names.
- Using underscores in class names.
- Naming methods with nouns instead of actions.
- Using meaningless variable names like `x`, `temp`, or `data`.
- Creating excessively long names.
- Using inconsistent naming styles.

---

## Best Practices

- Follow Java naming conventions consistently.
- Choose descriptive names.
- Keep names concise but meaningful.
- Prioritize readability over brevity.
- Maintain consistency throughout the project.

---

## Key Concepts Summary

- Packages use **lowercase**.
- Classes use **PascalCase**.
- Interfaces use **PascalCase**.
- Methods use **camelCase**.
- Variables use **camelCase**.
- Constants use **UPPER_SNAKE_CASE**.
- Java file names must match the public class name.

---

## Key Idea of this Chapter

Naming is one of the most important aspects of writing maintainable software.

Good names make code self-explanatory and reduce the need for excessive comments.

Professional developers spend time choosing names that communicate intent clearly.

---

## Summary

- Java defines official naming conventions for every language element.
- Consistent naming improves readability and collaboration.
- Packages, classes, methods, variables, and constants each follow specific conventions.
- Following these standards makes projects easier to maintain and understand.
- Good naming is a hallmark of professional software development.

---

## Next Step

**Chapter 8 — Your First Java Program**

In the next chapter, we will write our first Java application while understanding every part of the code, from the `main` method to program execution.
