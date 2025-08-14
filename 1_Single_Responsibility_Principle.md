# 📜 Single Responsibility Principle (SRP)

Let’s understand the **Single Responsibility Principle (SRP)** in a deep way so that you remember it for life.
Once you read this, you won’t need to revise it again.

---

## 1️⃣ Why is it Needed?

Software is never a one-day project. Over time, it goes through **updates**, **changes**, **bug fixes**, and **new features**.

If a class/module starts doing more than one type of job:

* ❌ Every small change can cause **side effects**
* ❌ Code becomes **hard to understand**
* ❌ **Maintenance time and cost** increase
* ❌ Testing takes longer because a change in one part can break another part

**SRP solves this problem** by saying — **a class should have only one responsibility**.

---

## 2️⃣ What is SRP?

📖 **Definition (Robert C. Martin):**

> “A class should have only one reason to change.”

💡 **Meaning:**

* A class should have **only one responsibility** (or purpose)
* If a class has more than one reason to change, it is violating SRP

🗣 **In simple words:**
If a person is an accountant, HR, and driver at the same time, mistakes will happen.
Same logic applies to code — one class should not try to do everything.

---

## 3️⃣ Without SRP – What Happens?

Example:

```java
public class Report {
    public void generateReport() {
        // logic to generate report
    }

    public void printReport() {
        // logic to print report
    }

    public void saveToDatabase() {
        // logic to save to database
    }
}
```

⚠ **Problems:**

1. **Tightly coupled code** – report generation, printing, and database saving are stuck in one class
2. **Multiple reasons to change** –

   * Change in report format → change in class
   * Change in print format → change in class
   * Change in database connection → change in class
3. **Hard to test** – testing one feature will load unrelated code
4. **Risk of breaking** – changing the print code could break the generation code

This creates a **God Class** — a class that tries to do everything.

---

## 4️⃣ After SRP – What Happens?

We create **separate dedicated classes/modules** for each task:

```java
public class ReportGenerator {
    public void generateReport() {
        // logic to generate report
    }
}

public class ReportPrinter {
    public void printReport() {
        // logic to print report
    }
}

public class ReportRepository {
    public void saveToDatabase() {
        // logic to save to database
    }
}
```

✅ **Benefits:**

1. **Single reason to change** –

   * ReportGenerator → only for generating reports
   * ReportPrinter → only for printing reports
   * ReportRepository → only for saving data
2. **Easier maintenance** – clear responsibilities
3. **Low risk** – changes in one part won’t break others
4. **Better testing** – each part can have its own unit test
5. **Reusability** – e.g., ReportPrinter can be reused in another project without extra code

---

## 💡 Real-life Analogy

Imagine a restaurant where:

🍽 **Without SRP:**
One person takes orders, cooks food, cleans tables, and handles payment → slow work, more mistakes, bad service.

🍽 **With SRP:**

* Waiter → takes orders
* Chef → cooks food
* Cleaner → cleans tables
* Cashier → handles payments

Result → faster work, better quality, fewer mistakes.

Software works the same way — **divide the responsibilities**.

---

## 📌 SRP Summary

> **One class → One job → One reason to change.**

---

## 🖥 Running Java Example

### 🚫 Without SRP

*(One class doing all tasks – God Class)*

```java
// Without SRP - One class doing too many things
public class Report {

    // 1. Generate report
    public void generateReport() {
        System.out.println("Generating report data...");
        // report generation logic
    }

    // 2. Print report
    public void printReport() {
        System.out.println("Printing report...");
        // printing logic
    }

    // 3. Save report to database
    public void saveToDatabase() {
        System.out.println("Saving report to database...");
        // database saving logic
    }

    public static void main(String[] args) {
        Report report = new Report();
        report.generateReport();
        report.printReport();
        report.saveToDatabase();
    }
}
```

---

#### ❌ Problems:

1. Multiple responsibilities — data generation, printing, and saving are all in one place
2. Multiple reasons to change — print format or database change will affect this class
3. Testing is hard — testing one method involves other unrelated methods
4. Low reusability — can’t reuse just the printing logic without taking everything

---

### ✅ With SRP

*(Each class has only one responsibility – clear separation of concerns)*

```java
// 1. Class to generate report
public class ReportGenerator {
    public void generateReport() {
        System.out.println("Generating report data...");
        // report generation logic
    }
}

// 2. Class to print report
public class ReportPrinter {
    public void printReport() {
        System.out.println("Printing report...");
        // printing logic
    }
}

// 3. Class to save report to DB
public class ReportRepository {
    public void saveToDatabase() {
        System.out.println("Saving report to database...");
        // database saving logic
    }
}

// Main class to use the above
public class MainApp {
    public static void main(String[] args) {
        ReportGenerator generator = new ReportGenerator();
        generator.generateReport();

        ReportPrinter printer = new ReportPrinter();
        printer.printReport();

        ReportRepository repository = new ReportRepository();
        repository.saveToDatabase();
    }
}
```

---

### ✅ Benefits:

1. **Single reason to change** —

   * ReportGenerator → only generates data
   * ReportPrinter → only handles printing
   * ReportRepository → only saves to database
2. Easy maintenance — changing one part doesn’t affect others
3. Better testing — each class can be tested separately
4. High reusability — any class can be reused in another project
5. Readable & scalable — new developers will understand responsibilities instantly

---

## 🎯 Final Takeaway

Without SRP → one person doing cooking, serving, and payment.
With SRP → each person handles one task.

Result → faster, cleaner, and safer code.

---

