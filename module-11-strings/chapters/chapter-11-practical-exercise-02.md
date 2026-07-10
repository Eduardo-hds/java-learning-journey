# Chapter 11 — Practical Exercise 02: Password Validator

## Chapter Objective

In this chapter, we will build a password validation system using String manipulation.

You will learn how to:

* Analyze characters inside a String
* Validate text rules
* Use `length()`
* Use `charAt()`
* Identify uppercase and lowercase letters
* Detect numbers
* Detect special characters
* Create reusable validation logic
* Separate responsibilities correctly

---

# 1. Why Password Validation?

Almost every application needs to validate user input.

Examples:

* registration systems
* login systems
* account creation
* security settings

A password usually needs rules like:

```text
Minimum length

Contains uppercase letter

Contains lowercase letter

Contains number

Contains special character
```

---

Example:

Valid:

```text id="x1y7v9"
Java@2026
```

Rules:

✅ 8+ characters
✅ Uppercase J
✅ Lowercase ava
✅ Numbers 2026
✅ Special character @

---

Invalid:

```text id="p4q8o1"
java
```

Problems:

❌ Too short
❌ No uppercase
❌ No number
❌ No special character

---

# 2. Project Structure

We continue using our architecture:

```text id="2w0q8x"
src/
 ├── Main.java
 ├── model/
 ├── service/
 │    ├── PalindromeChecker.java
 │    └── PasswordValidator.java
 └── util/
```

Responsibility:

```text id="4sk6z0"
Main

Receives password


PasswordValidator

Analyzes rules


Returns result
```

---

# 3. Creating PasswordValidator

Create:

```text id="8c2j3q"
service/
 └── PasswordValidator.java
```

Initial structure:

```java id="6n2s8d"
package service;

public class PasswordValidator {


}
```

---

# 4. Designing the Class

A password validator should answer:

> Is this password valid?

Therefore:

```java id="w0j3s8"
public boolean isValid(String password){

}
```

Returns:

```text id="o2t7i5"
true
```

or:

```text id="f9k3p1"
false
```

---

# 5. Rule 1 — Minimum Length

## Method

```java id="x4w8k2"
length()
```

returns the number of characters.

Example:

```java id="n8d5h4"
String password = "Java123";

System.out.println(
    password.length()
);
```

Output:

```text id="6x4m9q"
7
```

---

Validation:

```java id="5m7v9c"
password.length() >= 8
```

Meaning:

```text id="d8h2k6"
Password must have 8 or more characters
```

---

# 6. First Implementation

```java id="q9m1x5"
public boolean hasMinimumLength(String password){

    return password.length() >= 8;

}
```

---

Why separate methods?

Instead of:

```java id="f3y7m8"
if(
 length &&
 uppercase &&
 lowercase &&
 number
)
```

we create:

```text id="t9v5p3"
hasMinimumLength()

hasUppercase()

hasLowercase()

hasDigit()

hasSpecialCharacter()
```

Benefits:

* easier testing
* easier maintenance
* clearer code

---

# 7. Rule 2 — Detect Uppercase Letters

Example:

```text id="r5k1d8"
JAVA
```

Contains:

```text id="x3j9m4"
A-Z
```

---

Java provides:

```java id="m7q2x1"
Character.isUpperCase()
```

Example:

```java id="v4p6z8"
char letter = 'A';

System.out.println(
    Character.isUpperCase(letter)
);
```

Output:

```text id="u9d2c6"
true
```

---

# 8. Loop Through Characters

A String is a sequence of characters.

Example:

```text id="s8h3n2"
Java123
```

Indexes:

```text id="g7v5m1"
J a v a 1 2 3

0 1 2 3 4 5 6
```

We can inspect each character:

```java id="k8f4d9"
for(int i = 0; i < password.length(); i++){

    char c = password.charAt(i);

}
```

---

# 9. Implementing Uppercase Check

Logic:

```text id="j2p8q4"
Start:

hasUppercase = false


Check every character


If uppercase:

hasUppercase = true


Return result
```

---

Code:

```java id="r3x6w8"
public boolean hasUppercase(String password){

    for(int i = 0; i < password.length(); i++){

        char c = password.charAt(i);

        if(Character.isUpperCase(c)){

            return true;

        }

    }

    return false;

}
```

---

# 10. Rule 3 — Lowercase Letters

Same idea.

Method:

```java id="u7k5q2"
Character.isLowerCase()
```

Example:

```java id="z9x3c5"
public boolean hasLowercase(String password){

    for(int i = 0; i < password.length(); i++){

        char c = password.charAt(i);

        if(Character.isLowerCase(c)){

            return true;

        }

    }

    return false;

}
```

---

# 11. Rule 4 — Numbers

Java provides:

```java id="w3m7k9"
Character.isDigit()
```

Example:

```java id="f5q8n1"
char c = '5';

System.out.println(
    Character.isDigit(c)
);
```

Output:

```text id="q6j1v8"
true
```

---

Method:

```java id="s4d8p0"
public boolean hasDigit(String password){

    for(int i = 0; i < password.length(); i++){

        char c = password.charAt(i);

        if(Character.isDigit(c)){

            return true;

        }

    }

    return false;

}
```

---

# 12. Rule 5 — Special Characters

A special character is:

```text id="h3z7m9"
@ # $ % ! *
```

One simple approach:

```java id="y5k8d2"
if(
    !Character.isLetter(c)
    &&
    !Character.isDigit(c)
)
```

Meaning:

If it is not:

* a letter
* a number

then it is special.

---

Example:

```text id="c7p2w5"
A
```

Letter:

```text id="z8m4r1"
false
```

---

```text id="v3n9k6"
@
```

Not letter.

Not digit.

Therefore:

```text id="s2x6h8"
special character
```

---

Method:

```java id="p8j5v3"
public boolean hasSpecialCharacter(String password){

    for(int i = 0; i < password.length(); i++){

        char c = password.charAt(i);


        if(
            !Character.isLetter(c)
            &&
            !Character.isDigit(c)
        ){

            return true;

        }

    }


    return false;

}
```

---

# 13. Combining Validation Rules

Now:

```java id="d9x2q7"
public boolean isValid(String password){

    return
        hasMinimumLength(password)
        &&
        hasUppercase(password)
        &&
        hasLowercase(password)
        &&
        hasDigit(password)
        &&
        hasSpecialCharacter(password);

}
```

---

The password must pass:

```text id="e7q3w9"
Length
 +
Uppercase
 +
Lowercase
 +
Number
 +
Special
```

---

# 14. Testing From Main

Example:

```java id="h2m8z5"
import service.PasswordValidator;


public class Main {

    public static void main(String[] args) {


        PasswordValidator validator =
                new PasswordValidator();


        String password =
                "Java@2026";


        System.out.println(
            validator.isValid(password)
        );


    }

}
```

Output:

```text id="m5q7v2"
true
```

---

Testing:

```text id="x4n8k6"
java
```

Output:

```text id="p7d3m9"
false
```

---

# 15. Performance Consideration

Current implementation:

```java id="r8h2w5"
hasUppercase()

hasLowercase()

hasDigit()

hasSpecialCharacter()
```

Each method loops through the String.

Example:

Password:

```text id="z6p3x9"
20 characters
```

We may scan:

```text id="j5n7c2"
20
+
20
+
20
+
20
```

characters.

---

A more optimized solution:

One single loop:

```text id="a8m4k1"
Check all rules together
```

We will improve this later.

---

For learning:

The separated methods are better.

Why?

Because:

* clearer
* easier to understand
* easier to test

---

# 16. Common Mistakes

---

## Mistake 1 — Only checking length

Example:

```text id="w7q2d4"
abcdefgh
```

Length:

✅

Security:

❌

---

## Mistake 2 — Assuming numbers are enough

Example:

```text id="c5m8x1"
password123
```

Still weak.

Missing:

* uppercase
* special character

---

## Mistake 3 — Modifying the password

Never:

```java id="p9x3v7"
password = password.toLowerCase();
```

during validation.

You should validate the original value.

---

## Mistake 4 — Putting validation inside Main

Bad:

```java id="q4w8m2"
main(){

    check length

    check uppercase

    check digit

}
```

Better:

```text id="n8x5k3"
Main

↓

PasswordValidator
```

---

# Exercise Task

Implement:

```text id="v3m7q8"
service/
 └── PasswordValidator.java
```

Requirements:

Create:

```java id="x9p4d2"
public boolean isValid(String password)
```

Rules:

✅ Minimum 8 characters
✅ One uppercase
✅ One lowercase
✅ One digit
✅ One special character

Test:

Valid:

```text
Java@2026
```

Invalid:

```text
java
```

```text
JAVA1234
```

```text
Javaaaaa
```

---

# Chapter Summary

Today we learned:

✅ `length()` checks size
✅ `charAt()` accesses characters
✅ Strings can be analyzed character by character
✅ `Character` utility methods simplify validation
✅ Good design separates validation rules
✅ Services should contain business logic
✅ String analysis is the foundation of many applications

---

# Key Mental Model

A String:

```text id="z6h2n4"
"Java@2026"

↓

J a v a @ 2 0 2 6

↓

Analyze each character
```

---

# ✔️ Next Step

Proceed to:

# Chapter 12 — Practical Exercise 03: Word Counter

Next we will build a text analysis tool that can:

* Count words
* Count characters
* Count vowels
* Count consonants

We will combine:

* `split()`
* `length()`
* `charAt()`
* loops
* String analysis techniques.
