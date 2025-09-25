Usage Guide for Campus Course & Records Manager (CCRM)
Overview

Campus Course & Records Manager (CCRM) is a Java SE console application designed for managing campus records such as students, courses, enrollments, grades, transcripts, and file operations (import/export/backup). This menu-driven application provides various functionalities to add and manage campus data efficiently.

How to Set Up the Project
1. Clone the Repository

Clone the repository from GitHub using Git. Open Git Bash or Terminal and run the following command:

git clone https://github.com/AshwinGoyal713/vityarthi-java-project-.git


This will create a local copy of the project on your machine.

2. Install Java (JDK 17+)

Ensure that you have Java 17 or higher installed on your system. If not, download it from Oracle's website
 and follow the installation instructions.

3. Set Up the Project in Eclipse (Optional)

Create a new Java project in Eclipse.

Copy the src/ folder from the cloned repository into your new Eclipse project.

Run the application by right-clicking on MainCLI.java and selecting Run As > Java Application.

How to Run the Application
1. From Command Line (Without Eclipse)

If you're not using Eclipse, you can compile and run the project directly from the command line:

Navigate to the project directory (the one containing src/).

Compile the code:

javac -d bin src/edu/ccrm/**/*.java


Run the application:

java -cp bin edu.ccrm.cli.MainCLI


Enable Assertions (for debugging purposes):

java -ea -cp bin edu.ccrm.cli.MainCLI

Usage

When you run the application, you will be presented with the following main menu:

=====================================
  Welcome to Campus Course & Records Manager (CCRM)
=====================================

Main Menu:
1. Manage Students
2. Manage Courses
3. Manage Enrollments
4. Import / Export
5. Backup / Restore
6. Reports
7. Exit

Menu Options
1. Manage Students

Add Student: Allows you to add a new student by entering their registration number, name, and email.

List Students: Displays a list of all students in the system.

Deactivate Student: Deactivates a student using their registration number.

2. Manage Courses

Add Course: Allows you to add a new course with course code, title, and credits.

List Courses: Displays a list of all courses in the system.

3. Manage Enrollments

Enroll Student in Course: Allows students to enroll in courses, ensuring they don’t exceed the maximum credit limit (18 credits).

Unenroll Student: Allows you to unenroll a student from a specific course.

4. Import / Export

Import Data: Import student and course data from CSV files.

Export Data: Export current student and course data to CSV files.

5. Backup / Restore

Backup Data: Creates a backup of the student and course data in a timestamped folder.

Restore Data: Restores the system data from a backup.

6. Reports

Generate GPA Report: View GPA for each student.

Top Students Report: View the top students based on GPA.


Important Commands

Running the Program with Assertions:

Assertions are enabled by default for validation checks (e.g., ensuring that course credits are greater than 0). To run with assertions enabled:

java -ea -cp bin edu.ccrm.cli.MainCLI


Backup Folder: The backup data will be stored in the data/ folder, with a timestamp like backup_YYYY-MM-DD_HH-mm. Example:

data/backup_2023-10-05_15-30

Advanced Usage:

Import CSV Data: Use CSV files like students.csv and courses.csv to bulk load student and course data into the system. You can place these files in the data/ folder and use the Import menu option to load them.

Backup to a New Folder: The backup option will create a new folder in the data/ folder with a timestamp.

Run Reports: Generate reports to track GPA and the top-performing students using Streams and Lambdas.

Common Issues & Troubleshooting

"Max credits exceeded" error: If a student tries to enroll in courses exceeding max credits, the program will show an error.

File Permissions for Backup: Ensure you have write permissions for the data/ folder if you encounter issues with the backup functionality.

Conclusion

The CCRM project is a great way to demonstrate Java SE concepts like OOP, exception handling, file I/O, Streams, and collections. It’s designed to manage basic campus data without the complexity of databases, relying instead on files for storage.
