# Employee-Management-System
The Employee Management System is a relational database of tables and relationships of employee data in an organization
# Employee Management Database – SQL Project

## Overview

This SQL file creates and queries an **Employee Management Database** designed to store and analyze information about employees in an organization. The database contains tables for employee details, departments, job roles, salaries, attendance, and performance reviews.

The project demonstrates the use of **database creation, table relationships, data retrieval, filtering, sorting, joins, and pagination**.

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

---

## 2. Active Employees

```
SELECT *
FROM employees
WHERE Status = 'Active';
```

---

## 3. Employees Absent from Work

```
SELECT *
FROM attendance
WHERE Status = 'Absent';
```

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

---

## 5. Employees Earning Above 100,000

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
WHERE SalaryAmount > 100000;
```

---

## 6. Employees in HR and Finance Departments

```
SELECT *
FROM employees E
JOIN departments D
ON E.DepartmentID = D.DeptID
WHERE DeptName IN ('Human Resources', 'Finance');
```

---

## 7. Employees Not Active

```
SELECT *
FROM employees
WHERE Status != 'Active';
```

---

## 8. January 2026 Attendance Records

```
SELECT *
FROM employees E
JOIN attendance A
ON E.EmployeeID = A.EmployeeID
WHERE AttendanceDate LIKE '2026-01-%';
```

---

# Sorting and Ranking Queries

## Employees Sorted Alphabetically by Last Name

```
SELECT *
FROM employees
ORDER BY LastName;
```

---

## Employees with Highest Salaries

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
ORDER BY SalaryAmount DESC;
```

---

# Distinct Records

## Unique Departments

```
SELECT DISTINCT *
FROM departments;
```

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

---

# Observations on the Project

This project highlights the importance of understanding the **structure of database tables and the relationships between them**. Proper knowledge of these relationships is necessary to **import data in the correct order**, especially when foreign keys are involved. Doing so helps prevent errors and ensures that the database is created and populated successfully.


---

# Author

Opeyemi Morakinyo
