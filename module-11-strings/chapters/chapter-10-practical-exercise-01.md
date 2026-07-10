# Chapter 10 — Practical Exercise 01: Palindrome Checker

## Chapter Objective

In this chapter, we will begin applying our String knowledge in a real program.

You will learn how to:

* Analyze text character by character
* Compare characters inside a String
* Use `length()`
* Use `charAt()`
* Normalize user input
* Use `StringBuilder` for reverse operations
* Separate responsibilities into classes
* Build a small reusable component

---

# 1. What Is a Palindrome?

A palindrome is a word or sentence that reads the same forward and backward.

Examples:

Valid:

```text
level
```

Forward:

```text
level
```

Backward:

```text
level
```

Same result.

---

More examples:

```text
radar
```

```text
madam
```

```text
racecar
```

---

# 2. Sentence Palindromes

A sentence can also be a palindrome.

Example:

```text
Never odd or even
```

Ignoring:

* spaces
* capitalization

becomes:

```text
neveroddoreven
```

Reverse:

```text
neveroddoreven
```

Valid palindrome.

---

# 3. How Can We Check This?

There are multiple approaches.

---

## Approach 1 — Reverse the String

Example:

Original:

```text
Java
```

Reverse:

```text
avaJ
```

Compare:

```java id="c6d2k5"
original.equals(reverse)
```

If equal:

Palindrome.

---

## Approach 2 — Compare Characters

Instead of creating another String:

Compare:

```text
first character
with
last character
```

Example:

```text
level
```

Comparison:

```text
l == l

e == e

v == v
```

All match.

---

# 4. Choosing an Approach

For learning:

We will use both approaches.

First:

* use `StringBuilder.reverse()`

Then:

* create a manual algorithm using `charAt()`

This helps understand how String processing works internally.

---

# 5. Project Structure

Following our Bootcamp structure:

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 │    └── PalindromeChecker.java
 └── util/
```

Responsibility:

```text
Main
 |
 | receives input
 |
 v

PalindromeChecker
 |
 | analyzes text
 |
 v

boolean result
```

---

# 6. Creating the Service Class

Create:

```text
service/
 └── PalindromeChecker.java
```

The responsibility:

> Receive text and decide if it is a palindrome.

---

Initial structure:

```java
package service;

public class PalindromeChecker {


}
```

---

# 7. Creating the Method

We need something like:

```java
public boolean isPalindrome(String text){

}
```

Why boolean?

Because the result is only:

```text
true
```

or:

```text
false
```

---

Example:

```java
public boolean isPalindrome(String text){

    return true;

}
```

Temporary.

We will implement the logic.

---

# 8. Step 1 — Normalize the Text

Before checking:

Input:

```text
"Never Odd Or Even"
```

Should become:

```text
neveroddoreven
```

We need:

* remove spaces
* convert to lowercase

---

Using previous knowledge:

```java
text
    .replace(" ", "")
    .toLowerCase();
```

---

Example:

```java
String cleanText =
        text
        .replace(" ", "")
        .toLowerCase();
```

---

Before:

```text
Never Odd Or Even
```

After:

```text
neveroddoreven
```

---

# 9. Important Improvement

Only removing spaces is limited.

Example:

```text
"Never, odd or even!"
```

Contains:

```text
,
!
```

A more complete normalization:

```java
replaceAll("[^a-zA-Z]", "")
```

This uses regular expressions.

We are not studying Regex deeply now.

Understand only:

> Remove characters that are not letters.

---

For this exercise:

Use:

```java
replaceAll("[^a-zA-Z]", "")
```

---

# 10. Step 2 — Create the Reverse

Now:

```java
StringBuilder builder =
        new StringBuilder(cleanText);
```

Then:

```java
builder.reverse();
```

Convert:

```java
String reversed =
        builder.toString();
```

---

Example:

Original:

```text
neveroddoreven
```

Reverse:

```text
neveroddoreven
```

---

# 11. Step 3 — Compare

Now:

```java
return cleanText.equals(reversed);
```

Because:

We compare content.

Not:

```java
==
```

---

# 12. Complete Logic Flow

Conceptually:

```text
Original text

        |
        v

Normalize

        |
        v

Clean text

        |
        v

Reverse

        |
        v

Compare

        |
        v

true / false
```

---

# 13. Testing Through Main

Main:

```java
import service.PalindromeChecker;

public class Main {

    public static void main(String[] args) {

        PalindromeChecker checker =
                new PalindromeChecker();


        String text =
                "Never odd or even";


        boolean result =
                checker.isPalindrome(text);


        System.out.println(result);

    }
}
```

Expected:

```text
true
```

---

# 14. Testing Different Inputs

Input:

```text
level
```

Result:

```text
true
```

---

Input:

```text
Java
```

Result:

```text
false
```

---

Input:

```text
A man a plan a canal Panama
```

Result:

```text
true
```

---

# 15. Alternative Algorithm — Character Comparison

Now let's understand a more efficient approach.

Instead of:

```text
Create reverse String
Compare
```

we compare directly.

Example:

```text
radar
```

Indexes:

```text
r a d a r

0 1 2 3 4
```

Compare:

```text
index 0 with index 4

index 1 with index 3
```

Middle:

```text
index 2
```

does not need comparison.

---

# 16. Using `charAt()`

Remember:

```java
charAt(index)
```

gets a character.

Example:

```java
String word = "Java";

System.out.println(
    word.charAt(0)
);
```

Output:

```text
J
```

---

Indexes:

```text
J a v a

0 1 2 3
```

---

# 17. Manual Algorithm

Logic:

```text
Start:

left = 0

right = last position


while left < right:

compare characters

if different:
    not palindrome


move inward


finished:
    palindrome
```

---

Example:

```text
level
```

First:

```text
l == l
```

Move:

```text
e == e
```

Finished:

```text
true
```

---

# 18. Performance Comparison

## Reverse approach

Creates:

* cleaned String
* StringBuilder
* reversed String

Memory:

```text
More objects
```

---

## Character comparison

Uses:

* original String
* indexes

Memory:

```text
Less allocation
```

---

For small text:

Both are fine.

For huge text:

Character comparison is better.

---

# 19. Common Mistakes

---

## Mistake 1 — Using `==`

Wrong:

```java
return cleanText == reversed;
```

Correct:

```java
return cleanText.equals(reversed);
```

---

## Mistake 2 — Forgetting case differences

Example:

```text
Level
```

vs:

```text
level
```

Without normalization:

```text
false
```

---

## Mistake 3 — Ignoring spaces

Example:

```text
Never odd or even
```

Without cleaning:

```text
false
```

---

## Mistake 4 — Putting everything in Main

Bad:

```java
main(){

    normalize

    reverse

    compare

}
```

Better:

```text
Main
 |
 v
PalindromeChecker
```

---

# Exercise Task

Implement:

```text
service/
 └── PalindromeChecker.java
```

Requirements:

Create:

```java
public boolean isPalindrome(String text)
```

It must:

1. Remove unnecessary characters
2. Ignore uppercase/lowercase differences
3. Return true or false

Test:

```text
Never odd or even
level
Java
A man a plan a canal Panama
```

---

# Chapter Summary

Today we applied:

✅ String normalization
✅ `replace()`
✅ `toLowerCase()`
✅ `equals()`
✅ `StringBuilder`
✅ `reverse()`
✅ `charAt()`
✅ Service class organization

We also learned:

* A simple solution is not always the most memory-efficient
* String processing often involves creating intermediate objects
* Good design separates logic from input/output

---

# ✔️ Next Step

Proceed to:

# Chapter 11 — Practical Exercise 02: Password Validator

Next we will build a real validation service using Strings.

We will learn:

* Checking String length
* Searching characters
* Counting character types
* Building validation rules
* Creating reusable validation methods

This will prepare the foundation for the final **Text Processing Toolkit**.
