# Employee Management System

The **Employee Management System** is a simple database project that stores information about employees in a company.  
It keeps track of things like employee details, departments, job roles, salaries, attendance, and performance reviews.

This project was created using **SQL** to show how databases work and how data can be organized and analyzed.

---

# Project Overview

This SQL project creates a database and several tables that store employee information.

The project also includes SQL queries that help answer questions such as:

- Who are the active employees?
- Which employees work in a certain department?
- Which employees earn the highest salaries?
- Who are the top performers?

The project demonstrates important SQL concepts such as:

- Creating databases
- Creating tables
- Using relationships between tables
- Retrieving data
- Filtering results
- Sorting data
- Joining tables
- Limiting results (pagination)

---

# Database Name

`ProjectAss`

---

# Database Tables

The database has **6 main tables**.

Each table stores a different type of information.

---

## 1. Jobs Table

This table stores the different job roles in the company.

**Columns**

- `JobID` – Unique ID for each job
- `JobTitle` – Name of the job
- `MinSalary` – Minimum salary for the job
- `MaxSalary` – Maximum salary for the job

---

## 2. Departments Table

This table stores the departments in the organization.

**Columns**

- `DeptID` – Unique department ID
- `DeptName` – Name of the department
- `Location` – Where the department is located

Example departments could be:

- Finance
- Human Resources
- IT
- Marketing

---

## 3. Employees Table

This table stores information about every employee in the company.

**Columns**

- `EmployeeID` – Unique ID for each employee
- `FirstName`
- `LastName`
- `DateOfBirth`
- `Gender`
- `Email`
- `PhoneNumber`
- `HireDate`
- `JobID` – Links to the Jobs table
- `DepartmentID` – Links to the Departments table
- `ManagerID` – Links to another employee who is the manager
- `Status` – Shows if the employee is **Active, Inactive, or On Leave**

---

## 4. Salaries Table

This table stores salary records for employees.

This helps track salary changes over time.

**Columns**

- `SalaryID` – Unique salary record ID
- `EmployeeID` – Links to the Employees table
- `SalaryAmount`
- `FromDate` – When the salary started
- `ToDate` – When the salary ended

---

## 5. Attendance Table

This table tracks employee attendance.

**Columns**

- `AttendanceID`
- `EmployeeID`
- `AttendanceDate`
- `Status` – Present, Absent, or Leave
- `CheckInTime`
- `CheckOutTime`

---

## 6. Performance Table

This table stores employee performance reviews.

**Columns**

- `PerformanceID`
- `EmployeeID`
- `ReviewDate`
- `Rating` – Score from **1 to 5**
- `Comments` – Feedback about the employee

---

# Table Relationships

The tables are connected using **foreign keys**.

This allows the database to link related information together.

Examples:

- Employees are linked to jobs
- Employees are linked to departments
- Salaries belong to employees
- Attendance records belong to employees
- Performance reviews belong to employees

These connections help the system organize data properly.

---

# Checking Table Structure

The SQL script checks the structure of tables using the command:

```sql
DESCRIBE Employees;
DESCRIBE Departments;
DESCRIBE Jobs;
DESCRIBE Salaries;
DESCRIBE Attendance;
DESCRIBE Performance;

