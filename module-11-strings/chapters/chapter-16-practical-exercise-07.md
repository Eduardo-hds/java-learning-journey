# Chapter 16 — Practical Exercise 07: Text Statistics (Final Exercise Before the Project)

## Chapter Objective

This chapter brings together almost everything you've learned throughout Module 11.

By the end of this chapter, you will be able to:

* Combine multiple String operations into one analysis
* Create a model class to represent statistics
* Generate formatted reports
* Reuse existing services
* Follow good object-oriented design
* Prepare the core of the final project

This is the capstone exercise before the **Text Processing Toolkit**.

---

# 1. The Problem

So far, our `StringAnalyzer` can answer individual questions:

```java
analyzer.countWords(text);

analyzer.countCharacters(text);

analyzer.countVowels(text);

analyzer.countConsonants(text);
```

This works.

But imagine a real application.

Would you rather write:

```java
System.out.println(analyzer.countCharacters(text));
System.out.println(analyzer.countWords(text));
System.out.println(analyzer.countVowels(text));
System.out.println(analyzer.countConsonants(text));
```

Or simply:

```java
TextStatistics statistics =
        analyzer.generateStatistics(text);

System.out.println(statistics);
```

The second approach is cleaner and easier to extend.

---

# 2. Designing the Solution

Instead of returning many independent values, we'll create an object that groups them.

Project structure:

```text
src/
 ├── Main.java
 ├── model/
 │    ├── User.java
 │    └── TextStatistics.java
 ├── service/
 │    ├── StringAnalyzer.java
 │    ├── ReportBuilder.java
 │    └── ...
 └── util/
```

Responsibilities:

```text
Main

↓

StringAnalyzer

↓

TextStatistics

↓

ReportBuilder

↓

Formatted Report
```

Notice how each class has one responsibility.

---

# 3. Creating the Model

Create:

```text
model/
 └── TextStatistics.java
```

Suggested fields:

```java
private int characterCount;
private int wordCount;
private int vowelCount;
private int consonantCount;
private double averageWordLength;
private String longestWord;
private String shortestWord;
```

This class **stores data only**.

It should not analyze text.

---

# 4. Why Create a Model?

Without a model:

```java
int characters;
int words;
int vowels;
int consonants;
double average;
String longest;
String shortest;
```

Many variables spread across the application.

With a model:

```java
TextStatistics statistics;
```

Everything stays together.

This improves:

* readability
* maintainability
* scalability

---

# 5. Generating Statistics

Add a new method:

```java
public TextStatistics generateStatistics(String text)
```

Conceptually:

```text
Receive text

↓

Normalize

↓

Count characters

↓

Count words

↓

Count vowels

↓

Count consonants

↓

Find longest word

↓

Find shortest word

↓

Calculate average

↓

Return TextStatistics
```

Notice that this method **coordinates** the analysis by calling smaller methods you already implemented.

---

# 6. Reusing Existing Methods

Avoid rewriting code.

Instead:

```java
statistics.setCharacterCount(
        countCharacters(text)
);

statistics.setWordCount(
        countWords(text)
);

statistics.setVowelCount(
        countVowels(text)
);

statistics.setConsonantCount(
        countConsonants(text)
);
```

This is one of the main benefits of creating small, reusable methods.

---

# 7. Finding the Longest Word

Example:

```text
Java is an amazing language
```

Words:

```text
Java
is
an
amazing
language
```

Longest:

```text
language
```

Algorithm:

```text
Assume first word is longest

↓

Compare with every other word

↓

If current word is longer

↓

Replace longest
```

---

Example implementation:

```java
String longest = words[0];

for(String word : words){

    if(word.length() > longest.length()){

        longest = word;

    }

}
```

---

# 8. Finding the Shortest Word

Same idea.

Start:

```java
String shortest = words[0];
```

Loop:

```java
if(word.length() < shortest.length()){

    shortest = word;

}
```

---

Example:

```text
Java is powerful
```

Shortest:

```text
is
```

---

# 9. Calculating Average Word Length

Formula:

```text
Total letters

──────────────

Number of words
```

Important:

Do **not** count spaces.

Example:

```text
Java is fun
```

Letters:

```text
Java

↓

4

is

↓

2

fun

↓

3
```

Total:

```text
9
```

Words:

```text
3
```

Average:

```text
3.0
```

---

Suggested implementation:

```java
int totalLetters = 0;

for(String word : words){

    totalLetters += word.length();

}

double average =
        (double) totalLetters / words.length;
```

Notice the cast:

```java
(double)
```

Without it, Java would perform integer division.

---

# 10. Building the Report

Now create a formatted report.

Example:

```text
========== TEXT STATISTICS ==========

Characters : 24
Words      : 4
Vowels     : 8
Consonants : 13

Average Word Length : 5.25

Longest Word  : Programming
Shortest Word : Is

=====================================
```

---

# 11. ReportBuilder

Instead of printing inside `Main`, create:

```java
public String buildStatisticsReport(
        TextStatistics statistics)
```

Inside:

Use:

```java
StringBuilder
```

This reinforces everything learned in previous chapters.

---

# 12. Testing

Input:

```text
Java is powerful
```

Expected:

```text
Characters : 16
Words      : 3
Vowels     : 6
Consonants : 9
Longest    : powerful
Shortest   : is
Average    : 5.0
```

---

Another example:

```text
Spring Boot makes development easier
```

Expected:

Correct counts based on your implementation.

The exact formatting is less important than correct analysis.

---

# 13. Design Improvements

Notice our architecture now:

```text
Main

↓

StringAnalyzer

↓

TextStatistics

↓

ReportBuilder

↓

Console
```

Main is becoming very small.

That's a good sign.

Business logic belongs in services.

Presentation belongs in report builders.

Data belongs in models.

---

# 14. Performance Discussion

Current implementation performs multiple passes through the text.

Example:

* Count vowels
* Count consonants
* Find longest word
* Find shortest word

Could all of this be done in one pass?

Yes.

Would it be faster?

Yes.

Should we do that now?

Not necessarily.

At this stage, **clarity is more important than micro-optimization**.

A clear implementation is easier to debug and maintain.

---

# 15. Common Mistakes

### Mistake 1 — Duplicating Code

Don't rewrite the counting logic inside `generateStatistics()`.

Reuse:

```java
countWords()

countCharacters()

countVowels()

countConsonants()
```

---

### Mistake 2 — Dividing by Zero

If the text is empty:

```text
""
```

There are:

```text
0 words
```

Avoid:

```java
totalLetters / 0
```

Always check:

```java
if(wordCount == 0)
```

before calculating the average.

---

### Mistake 3 — Assuming the First Word Exists

If the text is empty:

```java
words[0]
```

throws an exception.

Validate the input first.

---

### Mistake 4 — Printing Inside the Analyzer

Bad:

```java
System.out.println(...)
```

inside `StringAnalyzer`.

The analyzer should **analyze**, not display information.

---

# Exercise Task

Create:

```text
model/
 └── TextStatistics.java
```

Update:

```text
service/
 └── StringAnalyzer.java
```

Implement:

```java
generateStatistics(String text)
```

Create:

```text
service/
 └── ReportBuilder.java
```

Implement:

```java
buildStatisticsReport(TextStatistics statistics)
```

Use:

* `StringBuilder`
* Existing counting methods
* Longest-word algorithm
* Shortest-word algorithm
* Average-word calculation

---

# Final Challenge

Test with:

```text
Java is an object oriented programming language
```

Verify:

* Characters
* Words
* Longest word
* Shortest word
* Average length

Try another example of your own and compare the results manually to ensure your implementation is correct.

---

# Chapter Summary

Today you learned how to combine multiple String techniques into a complete analysis.

You applied:

* ✅ `split()`
* ✅ `length()`
* ✅ `charAt()`
* ✅ `substring()`
* ✅ `StringBuilder`
* ✅ loops
* ✅ object-oriented design
* ✅ model classes
* ✅ service classes
* ✅ report generation

This chapter represents the culmination of everything covered in Module 11.

---

# Key Mental Model

Think of the flow as a pipeline:

```text
Raw Text
    │
    ▼
Normalize
    │
    ▼
Analyze
    │
    ▼
TextStatistics Model
    │
    ▼
ReportBuilder
    │
    ▼
Formatted Report
```

Each class has a single responsibility, making the application easier to extend and maintain.

---

# ✔️ Next Step

Proceed to:

# Final Project — Text Processing Toolkit

You now have all the building blocks needed to develop the module's final project.

The project will integrate:

* Text formatting
* Password validation
* Palindrome checking
* Word statistics
* String comparison
* Efficient report generation using `StringBuilder`

using the same package organization and design principles practiced throughout this module. After completing the project, we'll generate the standardized **Module Completion Report** for your Bootcamp Central Control chat.
