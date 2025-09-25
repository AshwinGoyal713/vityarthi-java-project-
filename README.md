# Campus Course & Records Manager (CCRM)

Hey, this is my Java SE console app for managing campus stuff—students, courses, enrollments, grades, transcripts, and basic file ops like import/export/backup. It's menu-driven: you pick numbers to add data, enroll students (with a max 18-credit rule that throws an exception if you overdo it), assign grades, compute GPAs, or back up to a folder. I built it to cover the syllabus topics, focusing on OOP, flow control, exceptions, collections, and I/O streams. No database (JDBC/JPA not needed for this local setup), but everything else is in there.


## How to Run the Project

### JDK Version
- Built/tested with **Java 17+ SE** (I used 21—works great for Streams and LocalDateTime).

### Commands (from project root)
1. **Compile**: 
   ```bash
   javac -d bin src/edu/ccrm/**/*.java
   ```
   (Puts .class files in bin—quick and simple.)

2. **Run**:
   ```bash
   java -cp bin edu.ccrm.cli.MainCLI
   ```
   (Shows welcome, loads sample data, menu appears.)

3. **With assertions enabled** (for debugging, e.g., checks credits > 0):
   ```bash
   java -ea -cp bin edu.ccrm.cli.MainCLI
   ```
   (Assertions only fire with -ea—handy for invariants like non-null regNo.)

### Eclipse Setup
1. Download Eclipse IDE (Java Developers) from eclipse.org > Extract/run > Pick workspace folder.
2. File > New > Java Project > Name: "CCRM" > Uncheck "Create module-info.java" > Finish.
3. Right-click src > New > Package > edu.ccrm.cli (repeat for domain/service/etc.) > Paste code files.
4. Right-click MainCLI.java > Run As > Java Application.
   - For assertions: Run Configurations > Arguments > VM arguments > Add "-ea" > Run.
5. Output: Console shows menu—try option 6 (reports) to see GPAs.

If issues: Refresh project (F5), clean (Project > Clean). I had a classpath hiccup first but fixed by adding src to build path.

## Evolution of Java (Short Timeline)
- **Java 1.0 (1995)**: Sun's debut—JVM/JRE/JDK born, "write once run anywhere" vs C/C++'s platform-specific compiles.
- **Java 1.1 (1997)**: Added inner classes/reflection; safer than C++ (no raw pointers).
- **Java 5 (2004)**: Generics/enums/autoboxing/for-each—fixed C++ template bugs, made loops cleaner.
- **Java 8 (2014)**: Lambdas/Streams/functional interfaces—huge for concise code (I used in reports).
- **Java 9 (2017)**: Modules for better packaging (skipped here—kept it simple).
- **Java 17 (2021)**: Records/sealed classes/LTS—modern, secure evolution from C++'s manual memory.

Java's grown from applets to cloud—beats C/C++ on portability/safety, but slower for low-level.

## Java ME vs SE vs EE Comparison

| Edition | Description | Example Use | Key Diffs |
|---------|-------------|-------------|-----------|
| **ME (Micro Edition)** | Lightweight, limited APIs (no full Streams/Collections). | Old mobiles/embedded (e.g., IoT devices). | Smaller than SE (no GUI/I/O extras); vs C++: less memory but no direct hardware access. Not used here—too basic. |
| **SE (Standard Edition)** | Core lang + libs (OOP, I/O, Threads). | Desktop/console apps like this (menus, files). | Full features vs ME (more libs); vs EE: no web/DB. I chose SE for local run—no server needed. |
| **EE (Enterprise Edition)** | SE + enterprise tools (servlets, JPA for DB). | Web/servers (e.g., Spring apps). | Heavier than SE (distributed); vs C++: managed scaling without crashes. Overkill for console—stuck to SE. |

SE was right: Handles syllabus topics (e.g., Streams for reports) without extras.

## JDK/JRE/JVM Explanation
- **JDK (Java Development Kit)**: Full dev suite—javac compiler, javadoc, libs, + JRE. Compiles .java to .class bytecode (I used it here).
- **JRE (Java Runtime Environment)**: Runtime only—libs (e.g., java.util for Lists) + JVM, no compiler. Runs apps (download if no building).
- **JVM (Java Virtual Machine)**: Bytecode executor—JIT to machine code, GC memory, platform-bridge (Windows/Linux). Makes Java portable vs C/C++'s recompiles.

**Interaction**: .java code → JDK javac → .class bytecode → JRE loads → JVM runs (GC avoids C++ leaks). For CCRM: JDK builds, JRE/JVM runs menus/backups—JVM handles recursion/Streams seamlessly.

## Windows Installation Steps (with Screenshots)
I did this on Windows 11—took ~10 mins, but PATH was finicky (restarted cmd fixed it). Screenshots in `/screenshots` (take yours during setup).

1. **Install JDK**: oracle.com/java > JDK 17/21 Windows x64 > Download MSI > Run > Next/Next (default: C:\Program Files\Java\jdk-17).
   - ![JDK Install](screenshots/jdk-install.png) (Installer window).

2. **Environment Variables**: Start > "Edit the system environment variables" > Environment Variables > System vars > Path > Edit > New > Add `C:\Program Files\Java\jdk-17\bin` > OK.
   - Set JAVA_HOME: New var > Name: JAVA_HOME > Value: C:\Program Files\Java\jdk-17 > OK.
   - Restart cmd/PowerShell.

3. **Verify**: Cmd > `java -version` > Should output "java version '17.0.x'" or similar.
   - ![JDK Version](screenshots/jdk-version.png) (Cmd showing version).

4. **Eclipse Setup**: eclipse.org > Download "Eclipse IDE for Java Developers" > Extract > Run eclipse.exe > Workspace: Pick folder > File > New > Java Project > "CCRM" > Uncheck module > Finish.
   - Right-click src > New > Package > edu.ccrm.cli (etc.) > Paste code.
   - Run: Right-click MainCLI.java > Run As > Java Application.
   - Assertions: Run Configurations > Arguments > VM args > "-ea" > Apply > Run.
   - ![Eclipse Setup](screenshots/eclipse-setup.png) (Package Explorer with src expanded).
   - ![Program Run](screenshots/program-run.png) (Console with menu after run).
   - ![Backup Folder](screenshots/backup-folder.png) (File Explorer showing data/backup_YYYY-MM-DD_HH-mm folder).

Test: Run MainCLI—menu loads. If "java not recognized", double-check PATH (cmd: echo %PATH%). I screenshot my exact steps.

## Mapping Table: Syllabus Topic → File/Class/Method
Full syllabus coverage—topic by topic, with file/method + description. Focused on 1-5 (console app); 6 (DB) noted as N/A (file-based persistence instead). Justifications tie to code.

### 1. Java Introduction
| Topic | File/Class/Method | Description |
|-------|-------------------|-------------|
| Java Hello World | cli/MainCLI.main() | Prints "CCRM - Campus Course & Records Manager" + menu (basic System.out). |
| Java JVM, JRE, JDK | README (explanation) | Used JDK 17 to compile; JRE for run, JVM for execution (portable vs C/C++ native). Diff C/C++: Java bytecode/JVM vs direct machine code; no manual alloc/free. |
| Java Variables/Data Types | util/InputHelper.getInt() | Primitives (int value), objects (String prompt); LocalDateTime in domain/BasePerson. |
| Java Operators | service/InMemoryEnrollmentService.enroll() | Arithmetic (+ sum credits), relational (> MAX_CREDITS), logical (&& in filter). |
| Java Input/Output | cli/MainCLI.showMainMenu() (output), util/InputHelper.getString() (Scanner input). |
| Java Expressions & Blocks | domain/Grade.fromMarks() | Ternary/expressions in if (marks >=90 ? S : A); code blocks in methods. |
| Java Comment | All files | // (e.g., "Note: HashMap for speed"), /* */ in class docs. |

### 2. Java Flow Control
| Topic | File/Class/Method | Description |
|-------|-------------------|-------------|
| Java if...else | util/InputHelper.getInt() | If-else for NumberFormatException; nested in enroll() credit check. |
| Java switch Statement | cli/MainCLI.main() | Switch on int option (case 1: handleStudents(); default: error). |
| Java for Loop | service/InMemoryEnrollmentService.computeGPA() | Traditional for not direct, but for-each below. |
| Java for-each Loop | cli/MainCLI.showReports() | For-each on List<Student> (for (Student s : students)). |
| Java while Loop | cli/MainCLI.main() | While (keepGoing) for menu loop. |
| Java break Statement | util/FolderUtils.listFilesRecursively() | Break if depth >3 (recursion base). |
| Java continue Statement | service/InMemoryCourseService.searchByDept() | Implicit continue in stream filter (skip non-matches). |

### 3. Java Object-Oriented Programming
#### Java OOP (Basics)
| Topic | File/Class/Method | Description |
|-------|-------------------|-------------|
| Java Class/Objects | domain/Student | Class def, new Student(...) creates object. |
| Java Methods | domain/BasePerson.getFullName() | Instance/static methods (getters). |
| Java Constructor | domain/Student(...) | Parameterized ctor calls super; default not needed. |
| Java Strings | io/FileHandler.exportData() | split(","), equalsIgnoreCase, + concat. |
| Java Access Modifiers | domain/BasePerson: private regNo, public getRegNo(), protected active. |
| Java this keyword | domain/Student.ProfileView.print() | this.getFullName() in inner class. |
| Java final keyword | domain/Course.code (final for immutability). |
| Java Recursion | util/FolderUtils.listFilesRecursively() | Self-call with depth+1; base if depth>3. |
| Java instanceof | domain/BasePerson.equals() | if (!(o instanceof BasePerson)). |
| Java Single/Anonymous Class | domain/Student (single), util/FolderUtils (anonymous FileVisitor). |
| Java enum Class | domain/Semester (simple enum). |

#### Java OOP (Inheritance & Polymorphism)
| Topic | File/Class/Method | 
|-------|-------------------|
| Java Inheritance | domain/Student extends BasePerson. |
| Java Method Overriding | domain/Student.toString() overrides BasePerson. |
| Java super Keyword | domain/Student ctor: super(regNo, fullName, email, date). |
| Abstract Class/Method | domain/BasePerson abstract, abstract getType(). |
| Java Interfaces | service/StudentService (addStudent etc.). |
| Java Polymorphism (overloading/overriding) | toString overridden (runtime poly); ctors overloaded in Course. |
| Java Encapsulation | domain/BasePerson: private fields + public getters/setters. |

#### Java OOP (Other Types)
| Topic | File/Class/Method | 
|-------|-------------------|
| Nested & Inner Class | domain/Student.ProfileView (inner, accesses outer via this). |
| Java Static Class | config/SystemSetup (static getInstance). |
| Java Anonymous Class | util/FolderUtils.getFolderSizeRecursively() (new SimpleFileVisitor<>() {}). |
| Java Singleton | config/SystemSetup (private ctor, static instance). |
| Java enum Class | domain/Grade (fields/methods). |
| Java enum Constructor | domain/Grade(double points, int minMarks). |
| Java enum String | domain/Semester.toString() (enum values as strings). |
| Java Reflection | Not implemented (advanced; used instanceof instead for type checks). |

### 4. Java Exception Handling & Multithreading
#### Exception Handling
| Topic | File/Class/Method | 
|-------|-------------------|
| Java Exceptions | exception/StudentNotFoundException (checked, extends Exception). |
| Java Exception Handling | cli/MainCLI.handleStudents() (try-catch for findByRegNoOrThrow). |
| Java try...catch | service/InMemoryEnrollmentService.enroll() (try for NIO, catch IOException). |
| Java throw/throws | service/StudentService.findByRegNoOrThrow() throws StudentNotFoundException. |
| Java catch Multiple Exceptions | cli/MainCLI.handleEnrollments() (catch (StudentNotFoundException \| CourseNotFoundException e)). |
| Java Annotations Types | domain/BasePerson.toString() (@Override implicit). |

#### Multithreading
| Topic | File/Class/Method | 
|-------|-------------------|
| Introduction/Thread Creations | Not implemented (single-threaded console; could add Thread for backup, but not needed). |
| Thread Life Cycle/Methods | N/A (no threads—syllabus focus, but app is sequential). |
| Java Synchronization | N/A. |
| User-defined packages | All: package edu.ccrm.domain; etc. (custom hierarchy). |

### 5. Java List & I/O Streams
| Topic | File/Class/Method | 
|-------|-------------------|
| String classes/methods/ops | io/FileHandler.importData() (split, trim, + for lines). |
| 1-D Arrays & Ops | service/InMemoryStudentService.getAllStudents() (List as 1D array-like). |
| 2-D/Jagged Arrays & Ops | Not used (no matrices needed; Lists suffice). |
| Java Collections Framework | java.util.* (List/ArrayList in Student.enrollments, HashMap in services). |
| Java Collection Interface | service/StudentService.getAllStudents() returns Collection<List>. |
| Java List Interface | domain/Student.getEnrollments() returns List<Enrollment>. |
| Java ArrayList | domain/Student.enrollments = new ArrayList<>(). |
| Java Vector | Not used (ArrayList faster/non-sync). |
| Java Stack | Not used (no LIFO needed). |
| Byte/Char Streams | io/FileHandler.exportData() (Files.write for bytes; Scanner for char input). |
| Java I/O Streams | NIO.2 Files.readAllLines (char stream). |
| Java Reader/Writer | util/InputHelper (Scanner as Reader); System.out as Writer. |

### 6. Database Applications with JDBC & Java Persistence API
| Topic | File/Class/Method | 
|-------|-------------------|
| JDBC Layout/Connecting/Queries | Not implemented (console/file-based; used CSV/NIO.2 for persistence—no SQL/DB driver). Could add H2 in-memory DB later. |
| Submitting Queries/Results | N/A (Streams for in-memory "queries" like searchByDept). |
| JDBC Driver External | N/A. |
| Java Persistence API (JPA) | Not implemented (EE feature for ORM; SE files cover data storage here). |

## Notes on Enabling Assertions & Sample Commands
Assertions check code assumptions (e.g., credits >0)—off by default, but enable for testing (syllabus: debug invariants like non-null IDs).
- **Enable**: `java -ea -cp bin edu.ccrm.cli.MainCLI`.
- **Example**: In enroll(), `assert credits > 0 : "Credits must be >0";`—fails with AssertionError if invalid (only with -ea).
- **Why?**: Complements exceptions (e.g., throw for business errors, assert for dev checks like regNo != null in addStudent).

