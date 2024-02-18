# Database Migration Scripts

This repository has been created by Fuad Fataliyev for the 'Production Operation Management' Course Assignment 1, it contains three scripts:

1. Create Tables
2. Migration
3. Roll back


# Database Initialization and Data Importing Procedures

This section of the documentation covers the initial creation of the `STUDENTS` and `INTERESTS` tables in the PostgreSQL database, along with the process for importing data into these tables from text files.

## Table Creation

### STUDENTS Table

The `STUDENTS` table is designed to hold basic information about students, including a unique identifier, first name, and last name.

#### Schema Definition

```sql
CREATE TABLE STUDENTS (
  ST_ID SERIAL PRIMARY KEY,
  ST_NAME VARCHAR(20),
  ST_LAST VARCHAR(20)
);
```


ST_ID: Auto-incrementing integer serving as a unique identifier for each student.
ST_NAME: A string field to store the student's first name, up to 20 characters.
ST_LAST: A string field to store the student's last name, up to 20 characters.


INTERESTS Table
The INTERESTS table is used to store the interests of each student, linked to the STUDENTS table by a foreign key.

```sql
CREATE TABLE INTERESTS (
  STUDENT_ID INT REFERENCES STUDENTS(ST_ID),
  INTEREST VARCHAR(20)
);
```


STUDENT_ID: Integer that references the ST_ID of the STUDENTS table, establishing a relationship between the two tables.
INTEREST: A string field to store a particular interest of a student, up to 20 characters.

Data Importing

Importing into STUDENTS
Data will be imported into the STUDENTS table from a text file. The file should be formatted with space-separated values, with each line representing a record.

```sql
COPY STUDENTS(ST_ID, ST_NAME, ST_LAST) FROM '[file_path]/students.txt' WITH DELIMITER ' ';
```

Replace [file_path] with the absolute path to the interests.txt file on your system. 

For me it is:
```sql
/Users/fuadfatali/Desktop/Fuad_Fataliyev_13537_POM1/students.txt
```

Importing into INTERESTS
Similarly, data will be imported into the INTERESTS table from a text file, which should also be formatted with space-separated values.

COPY INTERESTS(STUDENT_ID, INTEREST) FROM '[file_path]/interests.txt' WITH DELIMITER ' ';

Replace [file_path] with the absolute path to the interests.txt file on your system.

For me it is:
```sql
/Users/fuadfatali/Desktop/Fuad_Fataliyev_13537_POM1/students.txt
```

Viewing Data

To verify the data has been imported correctly, the following SELECT statements can be run:

```sql
SELECT * FROM STUDENTS;
SELECT * FROM INTERESTS;
```
Notes

Ensure that the PostgreSQL server has read access to the specified file paths.
Verify the data format in the text files matches the expected schema structure before running the import commands.


## Migration Script

The `migration.sql` script performs the following actions:

1. Renames `ST_ID` column to `STUDENT_ID` in the `STUDENTS` table.
2. Changes the length of `ST_NAME` and `ST_LAST` columns in the `STUDENTS` table from `VARCHAR(20)` to `VARCHAR(30)`.
3. Transforms the `INTERESTS` table to use an array of strings to store interests and orders them by `STUDENT_ID`.

### How to Run

Execute the `migration.sql` script in your PostgreSQL database using:
```sql
psql -U username -d databasename -a -f migration.sql
```

Replace `username` and `databasename` with your PostgreSQL username and database name, respectively.



## Rollback Script

The `rollback.sql` script can revert the changes made by the `migration.sql` script.

### How to Run

Execute the `rollback.sql` script in your PostgreSQL database using:

```sql
psql -U username -d databasename -a -f rollback.sql
```

Replace `username` and `databasename` with your PostgreSQL username and database name, respectively.

## Notes

- Ensure you have a backup of your database before running these scripts.
- These scripts should be run during a maintenance window when the database is not in active use.


If you have any problem, or question feel free to contact with me: fuad0fataliyev0@outlook.com
You can also watch video before running codes: https://youtu.be/DZy_FfsQqxw

Best regards,
Fuad Fataliyev
