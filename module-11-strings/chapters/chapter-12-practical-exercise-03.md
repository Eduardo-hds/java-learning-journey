# Chapter 12 — Practical Exercise 03: Word Counter

## Chapter Objective

In this chapter, we will build a text analysis component capable of extracting statistics from a text.

You will learn how to:

* Count words using `split()`
* Count characters using `length()`
* Analyze individual characters using `charAt()`
* Identify vowels and consonants
* Handle spaces correctly
* Build reusable text analysis services
* Prepare the foundation for the final Text Processing Toolkit

---

# 1. Why Count Words and Characters?

Text analysis is extremely common.

Examples:

* document editors
* search engines
* messaging applications
* analytics systems
* writing tools

A simple text:

```text
Java is powerful
```

contains information:

```text
Words: 3

Characters: 16

Vowels: ?

Consonants: ?
```

---

# 2. Project Structure

Continue our architecture:

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 │    ├── PalindromeChecker.java
 │    ├── PasswordValidator.java
 │    └── StringAnalyzer.java
 └── util/
```

We will create:

```text
service/
 └── StringAnalyzer.java
```

Responsibility:

> Analyze text and return information about it.

---

# 3. Creating StringAnalyzer

Initial class:

```java
package service;

public class StringAnalyzer {


}
```

---

We need methods for different responsibilities:

```text
countWords()

countCharacters()

countVowels()

countConsonants()
```

---

Why separate methods?

Bad:

```java
analyzeEverything()
```

containing hundreds of lines.

Better:

```text
StringAnalyzer

 ├── countWords()
 ├── countCharacters()
 ├── countVowels()
 └── countConsonants()
```

Each method has one responsibility.

---

# 4. Counting Characters

## Basic Concept

The simplest statistic:

```text
How many characters exist?
```

Java already provides:

```java
length()
```

Example:

```java
String text = "Java";

System.out.println(
    text.length()
);
```

Output:

```text
4
```

---

Implementation:

```java
public int countCharacters(String text){

    return text.length();

}
```

---

# 5. What Does length() Count?

Important:

Spaces are characters.

Example:

```java
String text = "Java Programming";
```

Count:

```text
J a v a _ P r o g r a m m i n g
```

The space:

```text
_
```

also counts.

---

Result:

```text
16
```

---

# 6. Counting Words

Now:

```text
Java is powerful
```

Words:

```text
Java
is
powerful
```

Total:

```text
3
```

---

The easiest approach:

Use:

```java
split()
```

---

Example:

```java
String[] words =
    text.split(" ");
```

Result:

```text
[
"Java",
"is",
"powerful"
]
```

---

The number of words:

```java
words.length
```

---

Implementation:

```java
public int countWords(String text){

    String[] words =
            text.split(" ");

    return words.length;

}
```

---

# 7. Problem With Simple split()

Consider:

```text
"Java   Programming"
```

There are multiple spaces.

Using:

```java
split(" ")
```

may create empty elements.

Example:

```text
[
Java,
"",
"",
Programming
]
```

Wrong count:

```text
4
```

Expected:

```text
2
```

---

# 8. Better Normalization

Before splitting:

Remove unnecessary spaces.

Using:

```java
strip()
```

and:

```java
split("\\s+")
```

Conceptually:

> Split whenever there is one or more spaces.

---

Example:

```java
public int countWords(String text){

    String clean =
        text.strip();


    if(clean.isEmpty()){
        return 0;
    }


    String[] words =
        clean.split("\\s+");


    return words.length;

}
```

---

# 9. Why Check Empty Text?

Imagine:

```java
String text = "";
```

Without checking:

```java
text.split("\\s+")
```

can produce unexpected results.

Better:

```java
if(clean.isEmpty()){
    return 0;
}
```

---

# 10. Counting Vowels

A vowel:

```text
a
e
i
o
u
```

Example:

```text
Java
```

Characters:

```text
J a v a
```

Vowels:

```text
a
a
```

Count:

```text
2
```

---

# 11. Analyzing Characters

We already know:

```java
charAt()
```

Example:

```java
String text = "Java";

char c = text.charAt(0);
```

Result:

```text
J
```

---

Loop:

```java
for(int i = 0; i < text.length(); i++){

    char c = text.charAt(i);

}
```

---

# 12. Implementing Vowel Counter

Logic:

```text
Start counter = 0

For every character:

    convert to lowercase

    if vowel:
        counter++

Return counter
```

---

Code:

```java
public int countVowels(String text){

    int count = 0;


    for(int i = 0; i < text.length(); i++){

        char c =
            Character.toLowerCase(
                text.charAt(i)
            );


        if(
            c == 'a' ||
            c == 'e' ||
            c == 'i' ||
            c == 'o' ||
            c == 'u'
        ){

            count++;

        }

    }


    return count;

}
```

---

# 13. Why Convert to Lowercase?

Without:

```java
'A'
```

and:

```java
'a'
```

are different characters.

Example:

```text
A != a
```

Using:

```java
Character.toLowerCase()
```

normalizes both.

---

# 14. Counting Consonants

A consonant is:

A letter that is not:

* vowel

Example:

```text
Java
```

Letters:

```text
J
a
v
a
```

Consonants:

```text
J
v
```

Count:

```text
2
```

---

# 15. Important Rule

Numbers and symbols are not consonants.

Example:

```text
Java123!
```

Should count:

Letters only.

---

Implementation:

```java
public int countConsonants(String text){

    int count = 0;


    for(int i = 0; i < text.length(); i++){

        char c =
            Character.toLowerCase(
                text.charAt(i)
            );


        if(Character.isLetter(c)
            &&
           c != 'a'
            &&
           c != 'e'
            &&
           c != 'i'
            &&
           c != 'o'
            &&
           c != 'u'
        ){

            count++;

        }

    }


    return count;

}
```

---

# 16. Testing StringAnalyzer

Main:

```java
import service.StringAnalyzer;


public class Main {

    public static void main(String[] args) {


        StringAnalyzer analyzer =
            new StringAnalyzer();


        String text =
            "Java is powerful";


        System.out.println(
            analyzer.countCharacters(text)
        );


        System.out.println(
            analyzer.countWords(text)
        );


        System.out.println(
            analyzer.countVowels(text)
        );


        System.out.println(
            analyzer.countConsonants(text)
        );

    }

}
```

---

Expected:

```text
16
3
6
9
```

---

# 17. Improving the Design

Currently:

```java
analyzer.countWords(text)

analyzer.countCharacters(text)

analyzer.countVowels(text)
```

works.

But a real application might need:

```text
Text Statistics Report

Characters: 16
Words: 3
Vowels: 6
Consonants: 9
```

Later we will create:

```text
TextStatistics
```

to group these values.

---

# 18. Performance Analysis

For:

```java
countWords()
```

We create:

```text
String[]
```

because of:

```java
split()
```

---

For:

```java
countVowels()
```

we only scan characters:

```text
O(n)
```

Meaning:

If text doubles:

```text
100 chars
```

becomes:

```text
200 chars
```

the work doubles.

---

# 19. Common Mistakes

---

## Mistake 1 — Counting spaces as words

Wrong:

```java
text.split(" ")
```

without cleaning.

---

## Mistake 2 — Counting numbers as consonants

Wrong:

```text
Java123
```

The numbers are not letters.

---

## Mistake 3 — Forgetting uppercase vowels

Example:

```text
JAVA
```

Without normalization:

Only lowercase vowels count.

---

## Mistake 4 — Putting analysis logic in Main

Avoid:

```java
main(){

    count words

    count vowels

    count characters

}
```

Use:

```text
Main

↓

StringAnalyzer
```

---

# Exercise Task

Create:

```text
service/
 └── StringAnalyzer.java
```

Implement:

```java
countCharacters()

countWords()

countVowels()

countConsonants()
```

Test with:

### Example 1

```text
Java is powerful
```

Expected:

```text
Characters: 16
Words: 3
```

---

### Example 2

```text
Hello World
```

Expected:

```text
Words: 2
Vowels: 3
Consonants: 7
```

---

### Example 3

```text
Java123!
```

Expected:

```text
Letters only count for vowels/consonants
```

---

# Chapter Summary

Today we learned:

✅ `length()` counts characters
✅ `split()` helps count words
✅ `charAt()` allows character analysis
✅ `Character` methods simplify validation
✅ Text processing requires normalization
✅ Good classes separate responsibilities
✅ String analysis is built by combining simple operations

---

# Key Mental Model

A String is:

```text
"Java is powerful"

        ↓

J a v a _ i s _ p o w e r f u l

        ↓

Analyze each piece
```

---

# ✔️ Next Step

Proceed to:

# Chapter 13 — Practical Exercise 04: Text Formatter

Next we will build a formatter capable of:

* Capitalizing words
* Removing extra spaces
* Normalizing text
* Building formatted output with `StringBuilder`

This will be the first exercise that combines multiple String techniques together.
