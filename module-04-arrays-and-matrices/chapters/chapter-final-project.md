# 🏁 Module 04 — Final Project: Student Grade Management System 🎓

Now you will put everything together from this module:

* Arrays
* Traversal (for / for-each)
* Utility methods (`Arrays`)
* Matrices (2D arrays)
* Row/column processing

This is where the module becomes **real software logic**, not just exercises.

---

# 🎯 Project Goal

Create a **console-based system** that manages students and their grades using arrays and matrices.

---

# 📦 Project Structure (IMPORTANT)

We will build it step-by-step later, but the final system must support:

## 1. Data Storage

* Store multiple students
* Each student has multiple grades
* Use:

  * `int[]` for a student’s grades
  * `int[][]` for all students

---

## 2. Input Data (Fixed or Manual)

For now (no Scanner requirement yet unless you want), you can define:

```java
int[][] grades = {
    {8, 7, 9},
    {6, 10, 8},
    {9, 9, 10}
};
```

---

## 3. Student Average

For each student (row):

```java id="student_avg"
for (int i = 0; i < grades.length; i++) {
    int sum = 0;

    for (int j = 0; j < grades[i].length; j++) {
        sum += grades[i][j];
    }

    double avg = (double) sum / grades[i].length;
    System.out.println("Student " + i + " average: " + avg);
}
```

---

## 4. Class Average

```java id="class_avg"
int total = 0;
int count = 0;

for (int i = 0; i < grades.length; i++) {
    for (int j = 0; j < grades[i].length; j++) {
        total += grades[i][j];
        count++;
    }
}

double classAvg = (double) total / count;

System.out.println("Class average: " + classAvg);
```

---

## 5. Highest and Lowest Grade

```java id="min_max"
int max = grades[0][0];
int min = grades[0][0];

for (int i = 0; i < grades.length; i++) {
    for (int j = 0; j < grades[i].length; j++) {
        if (grades[i][j] > max) max = grades[i][j];
        if (grades[i][j] < min) min = grades[i][j];
    }
}

System.out.println("Max grade: " + max);
System.out.println("Min grade: " + min);
```

---

## 6. Search for a Grade

```java id="search_grade"
int target = 9;
boolean found = false;

for (int i = 0; i < grades.length; i++) {
    for (int j = 0; j < grades[i].length; j++) {
        if (grades[i][j] == target) {
            System.out.println("Found at student " + i + ", index " + j);
            found = true;
        }
    }
}

if (!found) {
    System.out.println("Grade not found.");
}
```

---

## 7. Matrix Report View

```java id="matrix_print"
for (int i = 0; i < grades.length; i++) {
    for (int j = 0; j < grades[i].length; j++) {
        System.out.print(grades[i][j] + " ");
    }
    System.out.println();
}
```

---

# 📊 What You Are Building (Final Output Concept)

Example output:

```
Student 0 average: 8.0
Student 1 average: 8.0
Student 2 average: 9.33

Class average: 8.44

Max grade: 10
Min grade: 6

Found at student 2, index 1

8 7 9
6 10 8
9 9 10
```

---

# ⚠️ Rules Reminder

* Only arrays and matrices
* No ArrayList / Collections
* No advanced OOP
* Console-based only
* Keep logic simple and clear

---

# 🚀 Final Challenge (Your Task)

Now implement the **full program in a single Java class**:

### Must include:

* matrix definition
* student average
* class average
* min/max
* search
* print report

---

# ✔️ End of Module 04

If you want, next step I can:

* Review your solution
* Refactor your code like a senior Java developer
* Or move you to **Module 05 (Methods & Modular Design)**
