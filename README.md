# DDM
**Exercise 1: Database Development Life Cycle**, 

### **Step 1: SQL CREATE DATABASE Statement**
```sql
-- Create a new database
CREATE DATABASE testDB;
```

### **Step 2: SQL DROP DATABASE Statement**
```sql
-- Drop the database (if needed)
DROP DATABASE testDB;
```

### **Step 3: SQL CREATE TABLE Statement**
```sql
-- Switch to the newly created database
\c testDB

-- Create a table named "Persons"
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);

-- Insert random values
INSERT INTO Persons (PersonID, LastName, FirstName, Address, City) 
VALUES (1, 'Doe', 'John', '123 Elm St', 'Springfield'),
       (2, 'Smith', 'Jane', '456 Oak St', 'Columbus');

-- Show table contents
SELECT * FROM Persons;
```

### **Step 4: Create Table Using Another Table**
```sql
-- Create a new table based on the "Persons" table
CREATE TABLE PersonsCopy AS 
SELECT * FROM Persons;

-- Show the copied table
SELECT * FROM PersonsCopy;
```

### **Step 5: SQL DROP TABLE Statement**
```sql
-- Drop the "PersonsCopy" table
DROP TABLE PersonsCopy;

-- Check that the table is dropped
\dt;
```

### **Step 6: SQL ALTER TABLE Statement**

#### ALTER TABLE - ADD Column
```sql
-- Add an "Email" column to the "Persons" table
ALTER TABLE Persons ADD Email varchar(255);

-- Update with random email values
UPDATE Persons SET Email = 'john.doe@example.com' WHERE PersonID = 1;
UPDATE Persons SET Email = 'jane.smith@example.com' WHERE PersonID = 2;

-- Show table contents after adding the column
SELECT * FROM Persons;
```

#### ALTER TABLE - DROP COLUMN
```sql
-- Drop the "Email" column
ALTER TABLE Persons DROP COLUMN Email;

-- Show table contents after dropping the column
SELECT * FROM Persons;
```

#### ALTER TABLE - ALTER/MODIFY COLUMN (Change Data Type)
```sql
-- Add a column DateOfBirth
ALTER TABLE Persons ADD DateOfBirth date;

-- Update with random birthdates
UPDATE Persons SET DateOfBirth = '1985-05-23' WHERE PersonID = 1;
UPDATE Persons SET DateOfBirth = '1990-11-15' WHERE PersonID = 2;

-- Modify the data type of "DateOfBirth" to just year
ALTER TABLE Persons ALTER COLUMN DateOfBirth TYPE varchar(4);

-- Show table contents after modifying the data type
SELECT * FROM Persons;
```

### **Step 7: SQL Constraints**

#### SQL NOT NULL on CREATE TABLE
```sql
-- Create a new table with NOT NULL constraints
CREATE TABLE Employees (
    EmployeeID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

-- Insert random values
INSERT INTO Employees (EmployeeID, LastName, FirstName, Age) 
VALUES (1, 'Johnson', 'Amy', 30),
       (2, 'White', 'David', 45);

-- Show the table after inserting values
SELECT * FROM Employees;
```

#### SQL NOT NULL on ALTER TABLE
```sql
-- Alter the "Age" column to enforce NOT NULL
ALTER TABLE Employees ALTER COLUMN Age SET NOT NULL;

-- Show table after enforcing NOT NULL constraint
SELECT * FROM Employees;
```

#### SQL UNIQUE Constraint

##### On CREATE TABLE
```sql
-- Create another table with a UNIQUE constraint
CREATE TABLE Projects (
    ProjectID int UNIQUE,
    ProjectName varchar(255)
);

-- Insert random values
INSERT INTO Projects (ProjectID, ProjectName) 
VALUES (1, 'AI Development'),
       (2, 'Web Redesign');

-- Show table contents
SELECT * FROM Projects;
```

##### On ALTER TABLE
```sql
-- Add a UNIQUE constraint to the "ProjectName" column
ALTER TABLE Projects ADD CONSTRAINT unique_project_name UNIQUE (ProjectName);

-- Show table contents after adding the constraint
SELECT * FROM Projects;
```

##### DROP a UNIQUE Constraint
```sql
-- Drop the UNIQUE constraint
ALTER TABLE Projects DROP CONSTRAINT unique_project_name;

-- Show table contents after dropping the constraint
SELECT * FROM Projects;
```

#### SQL PRIMARY KEY Constraint

##### On CREATE TABLE
```sql
-- Create a table with a PRIMARY KEY
CREATE TABLE Departments (
    DepartmentID int PRIMARY KEY,
    DepartmentName varchar(255)
);

-- Insert random values
INSERT INTO Departments (DepartmentID, DepartmentName) 
VALUES (1, 'HR'),
       (2, 'IT');

-- Show table contents
SELECT * FROM Departments;
```

##### On ALTER TABLE
```sql
-- Add a PRIMARY KEY on an existing table
ALTER TABLE Projects ADD PRIMARY KEY (ProjectID);

-- Show table contents after adding the primary key
SELECT * FROM Projects;
```

##### DROP a PRIMARY KEY Constraint
```sql
-- Drop the PRIMARY KEY constraint
ALTER TABLE Projects DROP CONSTRAINT Projects_pkey;

-- Show table contents after dropping the primary key
SELECT * FROM Projects;
```

#### SQL FOREIGN KEY on CREATE TABLE
```sql
-- Create a table with a FOREIGN KEY
CREATE TABLE Tasks (
    TaskID int PRIMARY KEY,
    TaskName varchar(255),
    ProjectID int,
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);

-- Insert random values
INSERT INTO Tasks (TaskID, TaskName, ProjectID) 
VALUES (1, 'Design UI', 2),
       (2, 'Backend Setup', 1);

-- Show table contents
SELECT * FROM Tasks;
```

---
##
##
## 3.

---

## **Exercise 3: Implement Database Using SQL Data Definition with Constraints**

---

### **1. Creating Tables with SQL Data Definition**

#### SQL CREATE DATABASE Statement
```sql
CREATE DATABASE labDB;
```

#### SQL DROP DATABASE Statement
```sql
DROP DATABASE labDB;
```

---

### **2. SQL CREATE TABLE Statement**

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);

-- Insert random values
INSERT INTO Persons (PersonID, LastName, FirstName, Address, City)
VALUES (1, 'John', 'Doe', '123 Elm St', 'Springfield'),
       (2, 'Jane', 'Smith', '456 Oak St', 'Columbus');

-- Show table contents
SELECT * FROM Persons;
```

---

### **3. Create Table Using Another Table**

```sql
CREATE TABLE TestTable AS 
SELECT LastName, FirstName FROM Persons;

-- Show table contents
SELECT * FROM TestTable;
```

---

### **4. SQL DROP TABLE Statement**

```sql
DROP TABLE TestTable;

-- Show remaining tables
\dt;
```

---

### **5. SQL ALTER TABLE Statement**

#### Add Column
```sql
ALTER TABLE Persons ADD Email varchar(255);

-- Insert values for the new column
UPDATE Persons SET Email = 'john.doe@example.com' WHERE PersonID = 1;
UPDATE Persons SET Email = 'jane.smith@example.com' WHERE PersonID = 2;

-- Show table contents after adding column
SELECT * FROM Persons;
```

#### Drop Column
```sql
ALTER TABLE Persons DROP COLUMN Email;

-- Show table contents after dropping the column
SELECT * FROM Persons;
```

#### Modify Column
```sql
ALTER TABLE Persons ALTER COLUMN Address TYPE text;

-- Show table contents after modifying the column
SELECT * FROM Persons;
```

---

### **6. SQL Constraints**

#### SQL NOT NULL on CREATE TABLE
```sql
CREATE TABLE Employees (
    EmployeeID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

-- Insert random values
INSERT INTO Employees (EmployeeID, LastName, FirstName, Age)
VALUES (1, 'John', 'Doe', 30),
       (2, 'Jane', 'Smith', 40);

-- Show table contents
SELECT * FROM Employees;
```

#### SQL NOT NULL on ALTER TABLE
```sql
ALTER TABLE Employees ALTER COLUMN Age SET NOT NULL;

-- Show table contents after adding NOT NULL constraint
SELECT * FROM Employees;
```

---

### **7. SQL UNIQUE Constraint**

#### SQL UNIQUE Constraint on CREATE TABLE
```sql
CREATE TABLE Products (
    ProductID int NOT NULL,
    ProductName varchar(255),
    UNIQUE (ProductName)
);

-- Insert random values
INSERT INTO Products (ProductID, ProductName)
VALUES (1, 'Laptop'),
       (2, 'Mobile');

-- Show table contents
SELECT * FROM Products;
```

#### SQL UNIQUE Constraint on ALTER TABLE
```sql
ALTER TABLE Products ADD UNIQUE (ProductID);

-- Show table contents
SELECT * FROM Products;
```

#### Drop a UNIQUE Constraint
```sql
ALTER TABLE Products DROP CONSTRAINT products_productname_key;

-- Show table contents after dropping UNIQUE constraint
SELECT * FROM Products;
```

---

### **8. SQL PRIMARY KEY Constraint**

#### SQL PRIMARY KEY on CREATE TABLE
```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PRIMARY KEY (OrderID)
);

-- Insert random values
INSERT INTO Orders (OrderID, OrderNumber)
VALUES (1, 12345),
       (2, 67890);

-- Show table contents
SELECT * FROM Orders;
```

#### SQL PRIMARY KEY on ALTER TABLE
```sql
ALTER TABLE Orders ADD PRIMARY KEY (OrderID);

-- Show table contents after adding PRIMARY KEY
SELECT * FROM Orders;
```

#### Drop a PRIMARY KEY Constraint
```sql
ALTER TABLE Orders DROP CONSTRAINT orders_pkey;

-- Show table contents after dropping PRIMARY KEY
SELECT * FROM Orders;
```

---

### **9. SQL FOREIGN KEY on CREATE TABLE**

```sql
CREATE TABLE Customers (
    CustomerID int PRIMARY KEY,
    LastName varchar(255),
    FirstName varchar(255),
    OrderID int,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

-- Insert random values
INSERT INTO Customers (CustomerID, LastName, FirstName, OrderID)
VALUES (1, 'John', 'Doe', 1),
       (2, 'Jane', 'Smith', 2);

-- Show table contents
SELECT * FROM Customers;
```

---

### **10. CHECK Constraints**

#### Create Table with a CHECK Constraint
```sql
CREATE TABLE ProductsWithCheck (
    ProductID int,
    ProductName varchar(255),
    Price numeric CHECK (Price > 0)
);

-- Insert random values
INSERT INTO ProductsWithCheck (ProductID, ProductName, Price)
VALUES (1, 'Laptop', 1000),
       (2, 'Mobile', 700);

-- Show table contents
SELECT * FROM ProductsWithCheck;
```

---

### **11. Default Values**

```sql
CREATE TABLE Suppliers (
    SupplierID int PRIMARY KEY,
    SupplierName varchar(255) NOT NULL,
    ContactName varchar(255) DEFAULT 'Unknown'
);

-- Insert random values, some with default contact name
INSERT INTO Suppliers (SupplierID, SupplierName)
VALUES (1, 'Tech Supplies'),
       (2, 'Home Goods', 'Emily Johnson');

-- Show table contents
SELECT * FROM Suppliers;
```

---

### **12. Add, Remove, and Modify Columns in Tables**

#### Add a Column
```sql
ALTER TABLE Products ADD COLUMN Description text;

-- Update with random values
UPDATE Products SET Description = 'Electronics product' WHERE ProductID = 1;
UPDATE Products SET Description = 'Mobile product' WHERE ProductID = 2;

-- Show table contents
SELECT * FROM Products;
```

#### Remove a Column
```sql
ALTER TABLE Products DROP COLUMN Description;

-- Show table contents after removing the column
SELECT * FROM Products;
```

#### Modify Column Data Type
```sql
ALTER TABLE Products ALTER COLUMN Price TYPE numeric(12, 2);

-- Show table contents after modifying the column
SELECT * FROM Products;
```

---

### **13. Rename a Column and Table**

#### Rename a Column
```sql
ALTER TABLE Products RENAME COLUMN ProductName TO ItemName;

-- Show table contents after renaming the column
SELECT * FROM Products;
```

#### Rename a Table
```sql
ALTER TABLE Products RENAME TO Items;

-- Show all tables after renaming
\dt;
```

---

### **14. DROP Column and DROP Constraint**

#### Drop Column
```sql
ALTER TABLE Items DROP COLUMN Price;

-- Show table contents after dropping the column
SELECT * FROM Items;
```

#### Drop Constraint
```sql
ALTER TABLE Items DROP CONSTRAINT items_pkey;

-- Show table contents after dropping the constraint
SELECT * FROM Items;
```

---

---

#

-
 
###
