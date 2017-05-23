# *SQL Summary
<hr><hr><hr>

### SQL statements

```
SELECT * FROM Customer;
```

### Important SQL Commands

```
* SELECT: extracts data from a database
* UPDATE: updates data in a database
* DELETE: delete data from a database
* INSERT INFO: inserts new data into a database
* CREATE DATABASE: creates a new database
* ALTER DATABASE: modifies a database
* CREATE TABLE: creates a new table
* ALTER TABLE: modifies a table
* DROP TABLE: delete a table
* CREATE INDEX: creates an index (search key)
* DROP INDEX: deletes an index
```

### SELECT

**select each column**

```
SELECT column1, column2,  
FROM table_name;
```

**select all**  

```
SELECT * FROM table_name;
```

**ex**

```
SELECT Customername, address from Customers;
```

### SQL SELECT DISTINCT

**select distinct column** (remove repeated column)

```
SELECT DISTINCT Country FROM Customers;
```

**select count column no.**

```
SELECT COUNT(DISTINCT Country) FROM Customers;
```
**select count column and change name**

```
SELECT COUNT(*) AS daham  
FROM Customers;
```

### SQL WHERE Clause

**WHERE clause is used to filter records**

```
SELECT * FROM Customers  
WHERE Country='Mexico';
```

**Operators in the WHERE Clause**

Operator|Description
|:---:|:---:|
=|Equal
<>|Not equal
|>|Greater than
<|Less than
|>=|Greater than or equal
|<=|Less than or equal
|BETWEEN|between an inclusive range
|LIKE|Search for a pattern
IN|To specify multiple possible values for a column


### SQL AND, OR, NOT Operators

**AND Syntax**

```
SELECT CustomerName FROM Customers
WHERE Country='Germany'AND CustomerID > 10;
```

**OR Syntax**

```
SELECT * FROM Customers
WHERE City='Berlin' OR City='München' OR CustomerID=4;
```
**NOT Syntax**

```
SELECT * FROM Customers
WHERE NOT Country='Germany';
```

**Combining Syntax**

```
SELECT * FROM Customers
WHERE Country='Germany'AND NOT City='Aachen';
```

### SQL ORDER 

**ORDER Statements**

```
SELECT * FROM Customers
ORDER BY Country;
```
**ORDER BY DESC Example (reversed order)**

```
SELECT * FROM Customers
ORDER BY Country DESC;
```

**ORDER BY Several Columns**

```
SELECT * FROM Customers
ORDER BY Country , ContactName;
```

```
SELECT * FROM Customers
ORDER BY Country ASC, CustomerID DESC;
```

### SQL INSERT INTO

**INSERT Syntax**

```
INSERT INTO Customers (CustomerName)
VALUES ('daham');
```

```
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

### NULL VALUE

**NULL Syntax**

>It is not possible to test for NULL values with comparison operators, such as =, <, <>   
We will have to use the IS NULL and IS NOT NULL operators instead.

```
SELECT *
FROM Customers
WHERE Contactname IS NULL;
```

### SQL UPDATE

**UPDATE Syntax**

```
UPDATE Customers
SET contactname='dahamlee', address='Cheonan'
WHERE CustomerID=100
```

**UPDATE multiple**

```
UPDATE Customers
SET customername='dawon'
WHERE customerID>90 and customerID<100
```

### SQL DELETE

**DELETE Syntax**

```
DELETE FROM customers
WHERE customerID =100;
```

### SQL SELECT TOP

>*It has difference in using different program*

**SQL Server**

```
SELECT TOP number|percent column_name(s)
FROM table_name
WHERE condition;
```

**MySQL**

```
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```
**Oracle**

```
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
```

**ex**

```
SELECT * FROM Customers
WHERE CustomerID>50
LIMIT 3;
```
```
SELECT TOP 3 * FROM Customers
WHERE Country='Germany';
```

### SQL MIN() and MAX()

**MIN , MAX Syntax**

```
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```
```
SELECT MAX(Price) AS LargestPrice
FROM Products;
```

### SQL COUNT(), AVG(), SUM()

**COUNT() Syntax**

```
SELECT COUNT(ProductID)
FROM Products;
```
```
SELECT COUNT(DISTINCT SupplierID)
FROM Products;
```

**AVG()**

```
SELECT AVG(Price)
FROM Products;
```
```
SELECT AVG(DISTINCT categoryid)
FROM Products;
```

**SUM()**

```
SELECT SUM(Quantity)
FROM OrderDetails;
```
```
SELECT SUM(distinct categoryID)
FROM products;
```

### SQL LIKE

**LIKE Syntax (starting with 'a')**

```
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

**LIKE Syntax (ending with 'a')**

```
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```

**LIKE Syntax (having 'or')**

```
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```

**LIKE Syntax (having 'r' in thrid posotion)**

> _ numbers are numbers of position

```
SELECT * FROM Customers
WHERE CustomerName LIKE '__r%';
```

> _ numbers also mean the number of character

```
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__% %__% %__% %__%';
```

**LIKE Syntax (not starting with 'a')**

```
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
```

### SQL Wildcard

* % - The percent sign represents zero, one, or multiple characters
* _ - THe underscore represents a single character


LIKE Operator|Description  
|:---:|:---:|
WHERE  CustomerName LIKE 'a%'|Finds any values that starts with "a"
WHERE CustomerName LIKE '%a'|Finds any values that ends with "a"
WHERE CustomerName LIKE '%or%'|Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%'|Finds any values that have "r" in the second position|
|WHERE CustomerName LIKE 'a_%_%'|Finds any values that starts with "a" and are at least 3 characters in length|
|WHERE ContractName LIKE 'a%o'|Finds any values that starts with "a" and ends with "o"


**% ex**

```
SELECT * FROM Customers
WHERE City LIKE 'ber%'; 
```

**_ex**

```
SELECT * FROM Customers
WHERE City LIKE '___in';
```

**Using the [charlist] Wildcard**
>Starting with every character in list

```
SELECT * FROM Customers
WHERE City LIKE '[bsp]%';
```

**Using the [!charlist] Wildcard**
>Not starting with characters in list

```
SELECT * FROM Customers
WHERE City LIKE '[!bsp]%';
```
```
SELECT * FROM Customers
WHERE City NOT LIKE '[bsp]%'; 
```

### SQL IN Operator

**IN Syntax**

```
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```
* _**IMPORTANT !!!!!!**_
```
SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers); 
```

### SQL BETWEEN Operator

>Same as price>=10 and price<=20
```
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20; 
```
>Text could be able to express
```
SELECT * FROM Products
WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY Productname;
```
>Dates expression
```
SELECT * FROM Orders
WHERE OrderDate BETWEEN #07/04/1996# AND #07/09/1996#;
```

### SQL Aliases

**Alias Column Syntax**
>Using 'AS'
```
SELECT CustomerID as ID, CustomerName AS Customer
FROM Customers; 
```
>If it contains 'space' than use square bracket
```
SELECT CustomerName AS Customer, ContactName AS [Contact Person]
FROM Customers;
```
>Combining columns into one column
```
SELECT CustomerName, Address +','+  PostalCode+','+ City+ ','+ Country as adresssss
FROM Customers;
```
>Using 'AS' in FROM
```
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName="Around the Horn" AND c.CustomerID=o.CustomerID; 
```
>Get data from each table
```
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName="Around the Horn" AND Customers.CustomerID=Orders.CustomerID; 
```



### SQL Joins
### -Inner Join

```
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID;
```
```
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```
```
SELECT Orders.OrderID, Customers.customername, Shippers.shippername
FROM ((Orders INNER JOIN Shippers On Orders.ShipperID=Shippers.shipperID) 
INNER JOIN Customers ON Orders.customerID=Customers.customerID)
ORDER BY OrderID;
```

### -Left Join

```
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```

### -Right Join
```
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID; 
```

### -Full outer join

```
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```


### SQL UNION

>Similar with using DISTINCT

```
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```

>UNION ALL (get all data even they are repeated)

```
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

### SQL GROUP BY
```
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```
```
SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;
```

### SQL HAVING
> Having is like IF

```
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```
```
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM (Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;
```

### SQL EXISTS ????
```
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price < 20);
```
```
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price = 22);
```

### SQL ANY and ALL ????

<hr>
<hr>
<hr>

# SQL DATABASE

## Create DATABASE

```
CREATE DATABASE databasename;
```

## SQL DROP DATABASE
**deleting database**

```
DROP DATABASE testDB;
```

## SQL CREATE TABLE

```
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```

## SQL DROP TABLE

**DROP TABLE (remove data and table itself)
```
DROP TABLE Shippers;
```

**TRUNCATE TABLE (remove data in table)

## SQL ALTER TABLE
**ADD COLUMN**

```
ALTER TABLE table_name
ADD column_name datatype;
```
**DROP COLUMN**

```
ALTER TABLE table_name
DROP COLUMN column_name;
```
**MODIFY COLUMN**

```
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

## SQL Contraints
**SQL Contraints**
   
* NOT NULL: ensures that a column cannot have a NULL value
* UNIQUE: ensures that all values in a column are different
* PRIMARY KEY: a combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* FOREIGN KEY: uniquely identifies a row/record in another table
* CHECK: ensures that all values in a column satisfies a specific condition
* DEFAULT: sets a default value for a column when no value is specified
* INDEX: use to create and retrieve data from the dataase very quickly

## -SQL NOT NULL
**when you put nothing it shows error**

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

## -SQL CHECK
**put options in column**

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

## -SQL DEFAULT
**put default value in column**

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);
```




