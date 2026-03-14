# Employee-Management-System
# Project Goal
The **Employee Management System** is a SQL database project designed to organize and manage employee information within an organization. The goal of this project is to demonstrate how relational databases can be used to store, connect, and analyze different types of employee data in a structured way.

The database stores important information such as employee details, departments, job roles, salary records, attendance history, and performance reviews. By organizing this information into separate tables and linking them together using relationships, the system makes it easier to manage large amounts of employee data efficiently.

This project was built using **SQL** and focuses on key database concepts such as database creation, table design, primary keys, foreign keys, and table relationships. It also demonstrates how SQL queries can be used to retrieve useful information from the database, including filtering records, sorting results, joining multiple tables, and limiting results for analysis.

Through this project, we can run queries to answer practical business questions such as identifying active employees, checking employee attendance, finding employees in specific departments, analyzing salary information, and identifying top-performing staff members.

Overall, the project serves as a practical example of how relational databases support data organization and decision-making in real-world organizations.

This project was created using **SQL** to show how databases work and how data can be organized and analyzed.

---


## Database Description

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

# Database Structure

The database contains **six main tables**:

### 1. Jobs

Stores job positions available in the organization.

**Columns**

* `JobID` – Unique identifier for each job
* `JobTitle` – Title of the job role
* `MinSalary` – Minimum salary for the job
* `MaxSalary` – Maximum salary for the job

---

### 2. Departments

Stores the departments within the organization.

**Columns**

* `DeptID` – Unique department identifier
* `DeptName` – Name of the department
* `Location` – Department location

---

### 3. Employees

Stores personal and employment information about employees.

**Columns**

* `EmployeeID` – Unique employee identifier
* `FirstName`
* `LastName`
* `DateOfBirth`
* `Gender`
* `Email`
* `PhoneNumber`
* `HireDate`
* `JobID` – References Jobs table
* `DepartmentID` – References Departments table
* `ManagerID` – References Employees table
* `Status` – Employment status (`Active`, `Inactive`, `On Leave`)

---

### 4. Salaries

Stores salary history for employees.

**Columns**

* `SalaryID` – Unique salary record
* `EmployeeID` – References Employees table
* `SalaryAmount`
* `FromDate`
* `ToDate`

---

### 5. Attendance

Tracks daily attendance records of employees.

**Columns**

* `AttendanceID`
* `EmployeeID` – References Employees table
* `AttendanceDate`
* `Status` – (`Present`, `Absent`, `Leave`)
* `CheckInTime`
* `CheckOutTime`

---

### 6. Performance

Stores employee performance review data.

**Columns**

* `PerformanceID`
* `EmployeeID` – References Employees table
* `ReviewDate`
* `Rating` – Performance rating between **1 and 5**
* `Comments`

---

# Database Relationships

The database uses **foreign keys** to maintain relationships:

* `Employees.JobID → Jobs.JobID`
* `Employees.DepartmentID → Departments.DeptID`
* `Employees.ManagerID → Employees.EmployeeID`
* `Salaries.EmployeeID → Employees.EmployeeID`
* `Attendance.EmployeeID → Employees.EmployeeID`
* `Performance.EmployeeID → Employees.EmployeeID`

These relationships allow the system to track employees across departments, job roles, salaries, attendance, and performance reviews.

---

# Key SQL Operations Demonstrated

## Table Structure Inspection

The script checks table structures using:

```
DESCRIBE Employees;
DESCRIBE Departments;
DESCRIBE Jobs;
DESCRIBE Salaries;
DESCRIBE Attendance;
DESCRIBE Performance;
```

---

# Data Retrieval Queries

## View Data in Tables

```
SELECT * FROM jobs;
SELECT * FROM departments;
SELECT * FROM employees;
SELECT * FROM attendance;
SELECT * FROM performance;
SELECT * FROM salaries;
```

---

# Example Analytical Queries

## 1. Employee Full Name and Email

Displays employee names and emails.

```
SELECT CONCAT(FirstName,' ', LastName) AS Full_name, Email
FROM employees;
```

### Query Result

[Download Employee Fullnae and Email](All%20employess%20fullname%20and%20email%20list.csv)
---

## 2. Active Employees

```
SELECT *
FROM employees
WHERE Status = 'Active';
```
[Active Employees CSV](active%20employees%20only.csv)
---

## 3. Employees Absent from Work

```
SELECT *
FROM attendance
WHERE Status = 'Absent';
```
[Download CSV File](absent employees.csv)
---

## 4. Active Employees in Finance Department

```
SELECT *
FROM employees E
JOIN departments D
ON D.DeptID = E.DepartmentID
WHERE DeptName = 'Finance'
AND Status = 'Active';
```
[Download CSV File](employees from the finance department who are still active.csv)
---

## 5. Employees Earning Above 100,000

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
WHERE SalaryAmount > 100000;
```
[Download CSV File](employee records who are paid above one hundred thousand.csv)
---

## 6. Employees in HR and Finance Departments

```
SELECT *
FROM employees E
JOIN departments D
ON E.DepartmentID = D.DeptID
WHERE DeptName IN ('Human Resources', 'Finance');
```
[Download CSV File](information about employees from the HR and Finance department.csv)
---

## 7. Employees Not Active

```
SELECT *
FROM employees
WHERE Status != 'Active';
```
[Download CSV File](Export records of employees aren’t active.csv)
---

## 8. January 2026 Attendance Records

```
SELECT *
FROM employees E
JOIN attendance A
ON E.EmployeeID = A.EmployeeID
WHERE AttendanceDate LIKE '2026-01-%';
```
[Download CSV File](attendance records of employees who were present in attendance only in Jan 2026.csv)
---

# Sorting and Ranking Queries

## Employees Sorted Alphabetically by Last Name

```
SELECT *
FROM employees
ORDER BY LastName;
```
[Download CSV File](Order Employees by last name in alphabetical Alphabetically.csv)
---

## Employees with Highest Salaries

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
ORDER BY SalaryAmount DESC;
```
[Download CSV File](records of employees with the Highest Salaries First.csv)
---

# Distinct Records

## Unique Departments

```
SELECT DISTINCT *
FROM departments;
```
[Download CSV File](Unique Departments in the organization.csv)
---

# Performance Analytics

## Top 5 Performers

```
SELECT *
FROM employees E
JOIN performance P
ON E.EmployeeID = P.EmployeeID
ORDER BY Rating DESC, ReviewDate DESC
LIMIT 0,5;
```
[Download CSV File](Top 5 Performers.csv)
---

# Pagination Example

## Next 5 Performers

```
SELECT *
FROM employees E
JOIN performance P
ON E.EmployeeID = P.EmployeeID
ORDER BY Rating DESC, ReviewDate DESC
LIMIT 5,5;
```

This query demonstrates **pagination**, retrieving records **6–10 after the first five**.
[Download CSV File](Next 5 Employees (Pagination).csv)
---

# Observations on the Project

This project highlights the importance of understanding the **structure of database tables and the relationships between them**. Proper knowledge of these relationships is necessary to **import data in the correct order**, especially when foreign keys are involved. Doing so helps prevent errors and ensures that the database is created and populated successfully.


---

# Author

Opeyemi Morakinyo
Business Intelligence Analyst | Sql | Excel | PowerBi
