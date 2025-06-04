# Schema

A **Schema** is the **logical blueprint** or **structure** of a database. It defines how data is organized and how the relationships between data are managed. It includes:
- **Tables**
- **Columns (fields)**
- **Data types**
- **Relationships**
- **Constraints** (like primary keys, foreign keys)\

> Schema is logical representation of database.
##  RDBMS Schema Example

When designing a schema in a **Relational Database Management System (RDBMS)**, you represent data using **tables** (also known as relations). Here's your example formatted with a clear schema definition:
#### Table: `Student`

| Column Name    | Data Type | Description                     |
| -------------- | --------- | ------------------------------- |
| Student_ID     | INT       | Unique identifier (Primary Key) |
| Student_Name   | VARCHAR   | Full name of the student        |
| Student_RollNo | INT       | Roll number in the class        |

####  Sample Data

| Student_ID | Student_Name     | Student_RollNo |
| ---------- | ---------------- | -------------- |
| 1          | Adarsh Pandey    | 101            |
| 2          | Ayush Pandey     | 102            |
| 3          | Nabhy Pandey     | 103            |
| 4          | Shreyansh Pandey | 104            |
