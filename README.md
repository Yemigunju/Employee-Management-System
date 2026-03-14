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

This query demonstrates **sorting**, displaying Active Employees
![employee names and emails]()

[Download Employee Fullname and Email](All%20employess%20fullname%20and%20email%20list.csv)
---

## 2. Active Employees

```
SELECT *
FROM employees
WHERE Status = 'Active';
```
This query demonstrates **sorting**, displaying Active Employees
[Download Active Employees](active%20employees%20only.csv)
---

## 3. Employees Absent from Work

```
SELECT *
FROM attendance
WHERE Status = 'Absent';
```
This query demonstrates **sorting**, displaying Employees Absent from Work
[Download Absent Employees Dataset](data/absent_employees.csv)
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
This query demonstrates **sorting**, displaying Active Employees in Finance Department
[Download Finance Department Active Employees Dataset](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/b293cd2ca5a636a34fb9db631991c329aee15e9d/employees%20from%20the%20finance%20department%20who%20are%20still%20active.csv)
---

## 5. Employees Earning Above 100,000

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
WHERE SalaryAmount > 100000;
```
This query demonstrates **sorting**, displaying Employees Earning Above 100,000
[Download employee records who are paid above one hundred thousand](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/e5ce472bd2ea45d981c452cf7505fbc5ff39b14a/employee%20records%20who%20are%20paid%20above%20one%20hundred%20thousand.csv)
---

## 6. Employees in HR and Finance Departments

```
SELECT *
FROM employees E
JOIN departments D
ON E.DepartmentID = D.DeptID
WHERE DeptName IN ('Human Resources', 'Finance');
```
This query demonstrates **sorting**, displaying Employees in HR and Finance Departments
[Download Employees in HR and Finance Departments](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/e5ce472bd2ea45d981c452cf7505fbc5ff39b14a/information%20about%20employees%20from%20the%20HR%20and%20Finance%20department.csv)
---

## 7. Employees Not Active

```
SELECT *
FROM employees
WHERE Status != 'Active';
```
This query demonstrates **sorting**, displaying Employees Not Active
[Download Employees Not Active CSV](https://github.com/Yemigunju/Employee-Management-System/raw/1db6fbfb78d706fcdedbedb38726014bcfee8711/Export%20records%20of%20employees%20aren%E2%80%99t%20active.csv)
---

## 8. January 2026 Attendance Records

```
SELECT *
FROM employees E
JOIN attendance A
ON E.EmployeeID = A.EmployeeID
WHERE AttendanceDate LIKE '2026-01-%';
```
This query demonstrates **sorting**, displaying January 2026 Attendance Records
[Download January 2026 Attendance Records CSV](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/fee5ea7058b250aad23a1c3f455225ef7087072d/attendance%20records%20of%20employees%20who%20were%20present%20in%20attendance%20only%20in%20Jan%202026.csv)
---

# Sorting and Ranking Queries

## Employees Sorted Alphabetically by Last Name

```
SELECT *
FROM employees
ORDER BY LastName;
```
This query demonstrates **sorting and ranking**, displaying Employees Sorted Alphabetically by Last Name
[Download Order Employees by last name in alphabetical Alphabetically.csv](https://github.com/Yemigunju/Employee-Management-System/blob/b96c7b77b4444db354917c0180bef7e4ca905102/Order%20Employees%20by%20last%20name%20in%20alphabetical%20Alphabetically.csv)
---

## Employees with Highest Salaries

```
SELECT *
FROM employees E
JOIN salaries S
ON E.EmployeeID = S.EmployeeID
ORDER BY SalaryAmount DESC;
```
This query demonstrates **sorting and ranking**, displaying Employees with Highest Salaries
[Download Employees with Highest Salaries CSV](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/b96c7b77b4444db354917c0180bef7e4ca905102/records%20of%20employees%20with%20the%20Highest%20Salaries%20First.csv)
---

# Distinct Records

## Unique Departments

```
SELECT DISTINCT *
FROM departments;
```
This query demonstrates **distinct records**, displaying the Unique Departments in the organization
[Download Unique Departments CSV](https://github.com/Yemigunju/Employee-Management-System/raw/b96c7b77b4444db354917c0180bef7e4ca905102/Unique%20Departments%20in%20the%20organization.csv)
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
This query demonstrates **ordering**, displaying the Top 5 Performers in the organization
[Download Top 5 Performers CSV](https://github.com/Yemigunju/Employee-Management-System/raw/bf4032478622728b642b1d2e3bd9fb5b6385958d/Top%205%20Performers.csv)
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
[Download Next 5 Performers CSV](https://raw.githubusercontent.com/Yemigunju/Employee-Management-System/1db6fbfb78d706fcdedbedb38726014bcfee8711/Next%205%20Employees%20(Pagination).csv)
---


## Tools Used

This Employee Management System project was built and analyzed using the following tools:

- **MySQL Workbench** – For creating the database, tables, and running SQL queries.
- **CSV Files** – For storing query results and exporting data for further analysis.
- **Markdown** – For writing and formatting the README file.
- **Screenshots / Image Editor** – For capturing query results and database schema visuals.
- **GitHub** – For version control and hosting the project repository online.
- **Excel** – For opening and analyzing CSV results.


# Observations on the Project

This project highlights the importance of understanding the **structure of database tables and the relationships between them**. Proper knowledge of these relationships is necessary to **import data in the correct order**, especially when foreign keys are involved. Doing so helps prevent errors and ensures that the database is created and populated successfully.


---

# Author

Opeyemi Morakinyo
Business Intelligence Analyst | Sql | Excel | PowerBi
