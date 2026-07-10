Here is a **final, clean, and professional version** of your `StudentSystem.java`, following exactly everything you learned in the module:

```java
import java.util.Scanner;

public class StudentSystem {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        // =========================
        // CONSTANTS (Business Rules)
        // =========================
        final double APPROVAL_GRADE = 6.0;

        // =========
        // INPUT
        // =========
        System.out.print("Enter full name: ");
        String name = scanner.nextLine();

        System.out.print("Enter age: ");
        int age = scanner.nextInt();

        System.out.print("Enter grade 1: ");
        double grade1 = scanner.nextDouble();

        if (grade1 < 0 || grade1 > 10) {
            System.out.println("Invalid input: grade must be between 0 and 10");
            scanner.close();
            return;
        }

        System.out.print("Enter grade 2: ");
        double grade2 = scanner.nextDouble();

        if (grade2 < 0 || grade2 > 10) {
            System.out.println("Invalid input: grade must be between 0 and 10");
            scanner.close();
            return;
        }

        // =========
        // PROCESSING
        // =========
        double average = (grade1 + grade2) / 2;

        String status;
        if (average >= APPROVAL_GRADE) {
            status = "Approved";
        } else {
            status = "Failed";
        }

        // =========
        // OUTPUT
        // =========
        System.out.println();
        System.out.println("========================");
        System.out.println("     STUDENT REPORT");
        System.out.println("========================");
        System.out.println();
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println();
        System.out.println("Grades:");
        System.out.println("- Grade 1: " + grade1);
        System.out.println("- Grade 2: " + grade2);
        System.out.println();
        System.out.printf("Average: %.2f%n", average);
        System.out.println("Status: " + status);
        System.out.println();
        System.out.println("========================");

        scanner.close();
    }
}
```
