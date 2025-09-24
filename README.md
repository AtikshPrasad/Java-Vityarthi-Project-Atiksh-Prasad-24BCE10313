# Java-Vityarthi-Project-Atiksh-Prasad-24BCE10313
# Campus Course & Records Manager (CCRM)

## 1. Project Overview

[cite_start]The Campus Course & Records Manager (CCRM) is a console-based Java SE application designed for an educational institute to manage student records, course information, enrollments, and grades. [cite: 4] [cite_start]It provides a command-line interface (CLI) for all administrative tasks and includes utilities for data import, export, and backup. [cite: 10, 35]

[cite_start]This project is built using Java SE and demonstrates a wide range of core Java concepts, including Object-Oriented Programming (OOP), modern I/O with NIO.2, the Streams API, the Date/Time API, exception handling, and common design patterns. [cite: 11, 12]

### How to Run the Project

1.  **Prerequisites:**
    * Java Development Kit (JDK) 11 or newer.
    * An IDE like Eclipse or IntelliJ IDEA, or a command-line interface.

2.  **Commands:**
    * **Compile:** Navigate to the `src` directory and run:
        ```bash
        javac edu/ccrm/cli/MainMenu.java
        ```
    * **Run:** From the `src` directory, run:
        ```bash
        java edu.ccrm.cli.MainMenu
        ```
    * [cite_start]**Enable Assertions:** To run with assertions enabled (as used in the project for invariant checks), use the `-ea` flag: [cite: 89]
        ```bash
        java -ea edu.ccrm.cli.MainMenu
        ```

---

## 2. Java Platform Documentation

### [cite_start]Evolution of Java (Short Timeline) [cite: 42]

* **1995:** Java 1.0 released by Sun Microsystems.
* **1998:** J2SE 1.2 released, introducing Swing, Collections Framework.
* **2004:** J2SE 5.0 (Tiger) released, adding Generics, Enums, Annotations, and Autoboxing.
* **2014:** Java SE 8 released, a major update introducing Lambda Expressions, the Stream API, and a new Date/Time API.
* **2017:** Java SE 9 introduced the Java Platform Module System.
* **2018:** Java SE 11 released as the second Long-Term Support (LTS) version after Java 8.
* **2021:** Java SE 17 becomes the latest LTS release, with features like Sealed Classes.

### [cite_start]Java ME vs Java SE vs Java EE [cite: 43]

| Feature           | Java ME (Micro Edition)                               | Java SE (Standard Edition)                                  | Java EE (Enterprise Edition)                                 |
| ----------------- | ----------------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| **Target** | Resource-constrained devices (e.g., mobile, embedded) | General-purpose desktop, server, and console applications | Large-scale, distributed, and web-based enterprise applications |
| **Core API** | A subset of Java SE API + specific libraries for mobile | The core Java programming platform (Core API, JVM, JDK)     | Built on top of Java SE; adds extensive libraries for enterprise |
| **Key Features** | Small footprint, specific profiles (e.g., CLDC, MIDP) | Collections, I/O, Networking, Swing, AWT, Concurrency       | Servlets, JSP, EJB, JPA, RESTful web services, Message Queues  |
| **Example App** | Old feature phone games                               | This CCRM project, desktop calculators, simple servers      | E-commerce websites, banking applications, airline portals     |

### [cite_start]Java Architecture: JDK, JRE, JVM [cite: 44]

* **JVM (Java Virtual Machine):** The JVM is an abstract computing machine that enables a computer to run a Java program. It interprets the compiled Java bytecode and executes it. The JVM is platform-dependent, which is how Java achieves its "write once, run anywhere" capability.
* **JRE (Java Runtime Environment):** The JRE is the software environment in which Java programs run. It contains the JVM, core Java libraries (like `java.lang`, `java.util`), and other components needed to execute a Java application. You need the JRE to *run* a Java program, but not to develop one.
* **JDK (Java Development Kit):** The JDK is a superset of the JRE. It contains everything in the JRE, plus development tools necessary to *create* Java programs. This includes the compiler (`javac`), debugger (`jdb`), and other utilities. To develop Java applications, you need the JDK.

**Interaction:** A developer writes Java code (`.java` file), uses the **JDK**'s compiler to turn it into bytecode (`.class` file), and this bytecode can then be executed on any machine that has a **JRE** installed, because the **JRE** contains the **JVM** to run that bytecode.

---

## 3. Setup and Configuration

### [cite_start]Install & Configure Java on Windows [cite: 45]

1.  Download the JDK installer (e.g., from Oracle or OpenJDK).
2.  Run the installer and follow the on-screen instructions.
3.  **Set Environment Variables:**
    * Find the JDK installation path (e.g., `C:\Program Files\Java\jdk-17`).
    * Open "System Properties" -> "Advanced" -> "Environment Variables".
    * Under "System variables", create a new variable `JAVA_HOME` and set its value to your JDK installation path.
    * Find the `Path` variable, click "Edit", and add a new entry: `%JAVA_HOME%\bin`.
4.  **Verification:** Open a new Command Prompt and run `java -version` and `javac -version`. You should see the installed version details.

[cite_start]**(Placeholder for your `java -version` screenshot)** [cite: 139]

### [cite_start]Using Eclipse IDE [cite: 46]

1.  **New Project Creation:**
    * Go to `File -> New -> Java Project`.
    * Enter a project name (e.g., `CCRM_Project`).
    * Select the appropriate JRE.
    * Click `Finish`.
2.  **Run Configuration:**
    * Right-click on the `MainMenu.java` file in the Package Explorer.
    * Select `Run As -> Java Application`. Eclipse will automatically create a run configuration.

[cite_start]**(Placeholder for your Eclipse project setup and run configuration screenshots)** [cite: 140]

---

## 4. Technical Demonstrations

### [cite_start]Justification: Interface vs. Abstract Class [cite: 71]

In this project, we used an **abstract class `Person`** and an **interface `Persistable`**.

* **Abstract Class `Person`:** `Student` and `Instructor` share common attributes (`id`, `fullName`, `email`) and behavior. An abstract class is suitable here because it establishes an "is-a" relationship (`Student is a Person`) and allows us to share code (fields and implemented methods), which an interface cannot do for fields.
* **Interface `Persistable`:** This interface defines a "can-do" capability: any class implementing it *can be* converted to a data format for saving. A `Student` can be persisted, a `Course` can be persisted. This is a behavior that is not tied to a common inheritance hierarchy, making an interface the perfect choice.

### [cite_start]Errors vs. Exceptions [cite: 83]

* **Errors:** Represent serious problems that a reasonable application should not try to catch. They are typically unrecoverable issues related to the runtime environment itself, such as `OutOfMemoryError` or `StackOverflowError`.
* **Exceptions:** Represent conditions that a program might want to catch and handle. They are further divided into:
    * **Checked Exceptions:** Conditions that a well-written application should anticipate and recover from (e.g., `FileNotFoundException`). The compiler forces you to handle them using `try-catch` or by declaring them with `throws`. [cite_start]Our custom `DuplicateEnrollmentException` is a checked exception. [cite: 87]
    * **Unchecked (Runtime) Exceptions:** Problems that arise from programming errors, such as `NullPointerException` or `IllegalArgumentException`. They are not required to be handled explicitly.

### [cite_start]Enabling Assertions [cite: 89, 137]

Assertions are used to check for invariants—conditions that should always be true. They are disabled by default. To enable them, use the `-ea` (enable assertions) flag when running the program from the command line:

```bash
java -ea edu.ccrm.cli.MainMenu
