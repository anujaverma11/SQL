/*  Code for "Introduction to T-SQL for Data Analysts using Microsoft SQL Server" */

/* START TASK 1 : Create a Database called "LearnSQL" */
CREATE DATABASE LearnSQL


/* START TASK 2a : Create a new Table called "Sales", with five columns within the  database */
USE [LearnSQL]
GO

CREATE TABLE "Sales" ("Account Manager ID" INT, "Sales ID" INT, "Category" VARCHAR(255), "SKU" VARCHAR(255), "Sales Price" MONEY)


/* START TASK 2b : Create a new table called "Staff" */
USE [LearnSQL]
GO

CREATE TABLE "Staff" ("Account Manager ID" INT, "First Name" VARCHAR(255), "Last Name" VARCHAR(255))


/* START TASK 3a : Load data into the "Sales" Table */
USE [LearnSQL]
GO

INSERT INTO Sales ([AccountManagerID], [SalesID], [Category], [SKU], [SalesPrice])
VALUES (1, 1, 'TVs', 'F600 Smart LED TV', 1209), (1, 2, 'TVs', 'F7001 Plasma TV', 999), (1, 3, 'TVs', 'F2300 LCD TV', 1800), (1, 4, 'TVs', 'F2300 LCD TV', 1800), (1, 5, 'TVs', 'F2300 LCD TV', 1800), (2, 6, 'Computer', 'X21 -Bus', 2399), (2, 7, 'GPS Navigation', 'Nav smart 2300', 435), (2, 8, 'GPS Navigation', 'Nav smart 2300', 435), (2, 9, 'Phones', 'G32 Phone', 499), (3, 10, 'Cameras', 'KL Mini Camera', 199), (3, 11, 'Cameras', 'KL Mini Camera', 199), (3, 12, 'Computer', 'X21 -Bus', 2399), (3, 13, 'GPS Navigation', 'Nav smart 2300', 435), (3, 14, 'TVs', '780 XC LCD TV', 699), (4, 15, 'Phones', 'G32 Phone', 499), (4, 16, 'Phones', 'G32 Phone', 499), (4, 17, 'Printers', 'MF 2400 Printer', 399), (4, 18, 'Printers', 'MF 2400 Printer', 399), (4, 19, 'Tablets', '10 Inch Maxi 2014', 799), (4, 20, 'TVs', 'F7001 Plasma TV', 999), (5, 20, 'TVs', 'F7001 Plasma TV', NULL), (6, 20, 'TVs', 'F7001 Plasma TV', 599)
GO


/* START TASK 3b: Load Data into the "Staff" Table */
USE [LearnSQL]
GO

INSERT INTO Staff ([Account Manager ID], [First Name], [Last Name])
VALUES (1, 'Billy', 'Murphy'), (2, 'Jeffrey', 'Wood'), (3, 'Judy', 'Allen'), (4, 'Evelyn', 'Mitchell'), (5, 'Bob', 'Smith'), (7, 'Mike', 'Williams')
GO


/* START TASK 4: Write a SELECT ALL query */
USE [LearnSQL]
GO

SELECT *
FROM Sales


/* START TASK 5 : SELECT  only data from the "Category" and "Sales Price" columns from the "Sales" table*/
USE [LearnSQL]
GO

SELECT Category, [Sales Price]
FROM Sales


/* START TASK 6 : Sort in Descending order */
USE [LearnSQL]
GO

SELECT *
FROM Sales
ORDER BY [Sales Price] DESC


/* START TASK 7: Select Unique Values  */
USE [LearnSQL]
GO

SELECT DISTINCT Category
FROM Sales


/* START TASK 8 : Selecting records greater than a value */
USE [LearnSQL]
GO

SELECT *
FROM Sales
WHERE [Sales Price] > 500


/* START TASK 9: Select the Top X Records in a Table  */
USE [LearnSQL]
GO

SELECT TOP (5) *
FROM Sales
ORDER BY [Sales Price] DESC


/* START TASK 10 : Wildcard searching for characters */
/* a "%" symbol  is a  substitute for zero or more characters. For example 'Cam%' will return cameras*/
/* the _ which is a  substitute for a single character. For example  '_ablets' */
/* the [] that provides a range of characters to match. For example '[C-G]%' */
/* The caret symbol inside square brackets provides  a set of characters not to match to. For example  '[^CP]%' */

USE [LearnSQL]
GO

SELECT *
FROM Sales
WHERE Category LIKE 'Cam%'


/* START TASK 11 : IN clause - specify multiple values in a WHERE clause */
USE [LearnSQL]
GO

SELECT *
FROM Sales
WHERE Category IN ('Computer', 'Printers', 'Tablets')


/* START TASK 12 : BETWEEN clause */
USE [LearnSQL]
GO

SELECT *
FROM Sales
WHERE [Sales Price] BETWEEN 500
    AND 1000


/* START TASK 13 : Selecting NULL values */
USE [LearnSQL]
GO

SELECT *
FROM [Sales]
WHERE [Sales Price] IS NULL


/* START TASK 14 : Selecting NON NULL values */
USE [LearnSQL]
GO

SELECT *
FROM [Sales]
WHERE [Sales Price] IS NOT NULL


/* START TASK 15: Combining filters  */
USE [LearnSQL]
GO

SELECT *
FROM Sales
WHERE [Sales Price] > 500
  OR [Category] LIKE 'C%'


/* START TASK 16 : Average by a GROUP & create column alias */
USE [LearnSQL]
GO

SELECT Category, AVG([Sales Price]) AS AvSalesPrice
FROM Sales
GROUP BY Category


/* START TASK 17 : Filtering groups based on aggregated values
2) WHERE clause is used for filtering rows and it applies on each and every row, while HAVING clause is used to filter groups in SQL. 3) One syntax level difference between WHERE and HAVING clause is that, former is used before GROUP BY clause, while later is used after GROUP BY clause
*/
USE [LearnSQL]
GO

SELECT Category, COUNT([Sales ID]) AS "Count IDs", SUM([Sales Price]) AS " Group Sales"
FROM [Sales]
GROUP BY Category
HAVING SUM([Sales Price]) > 500


/* START TASK 18: Join two columns from the "Staff" table into a new columnn (Concatenation) */
USE [LearnSQL]
GO

SELECT [First Name] + ' ' + [Last Name] AS [Full Name]
FROM [Staff]


/* START TASK 19 : Joining two tables with an "INNER JOIN" */
USE [LearnSQL]
GO

SELECT Staff.[First Name], Staff.[Last Name], Sales.Category, Sales.[Sales Price], Staff.[Account Manager ID], Sales.[Account Manager ID]
FROM Sales
INNER JOIN Staff
  ON Sales.[Account Manager ID] = Staff.[Account Manager ID]


/* START TASK 20 : Joining two tables with an "LEFT JOIN" */
SELECT Staff.[First Name], Staff.[Last Name], Sales.Category, Sales.[Sales Price], Staff.[Account Manager ID], Sales.[Account Manager ID]
FROM Sales
LEFT  JOIN Staff
  ON Sales.[Account Manager ID] = Staff.[Account Manager ID]


/* START TASK 21 : Joining two tables with an "RIGHT JOIN" */
SELECT Staff.[First Name], Staff.[Last Name], Sales.Category, Sales.[Sales Price], Staff.[Account Manager ID], Sales.[Account Manager ID]
FROM Sales
RIGHT JOIN Staff
  ON Sales.[Account Manager ID] = Staff.[Account Manager ID]


/* START TASK 22 : Creating a View */
USE LearnSQL
GO

CREATE VIEW FirstView
AS
SELECT Category, [Sales Price]
FROM [dbo].[Sales]


/* START TASK 23.  Create a Simple Stored Procedure called SimpleSP with a default parameter of 'Tablets'for the Category column  */
USE LearnSQL
GO

CREATE PROCEDURE SimpleSP @input_Parameter varchar(255) = 'Tablets'
AS
SELECT *
FROM Sales
WHERE Category = @input_Parameter


/* START TASK 24. To Execute Procedure with parameters */

EXEC SimpleSP 'Computer'



/* START TASK 25: Update Records */
USE [LearnSQL]
GO

UPDATE Sales
SET [Category] = 'Computers'
WHERE [Category] = 'Computer'


/* START TASK 26 : Backing-up a Table */
USE [LearnSQL]
GO

SELECT *
INTO Sales_Backup
FROM Sales


/* START TASK 27 : Deleting Specific values */
USE [LearnSQL]
GO

DELETE
FROM Sales_Backup
WHERE [Sales Price] > 500


/* START TASK 28  : Removing just the data from a table */
USE [LearnSQL]
GO

TRUNCATE TABLE Sales


/* START TASK 29 : DELETING a table */
USE [LearnSQL]
GO

DROP TABLE Sales


/* START TASK 30: DELETING a database */
/* Note don't include "USE" and "GO" syntax as you can't be connected to a database when you delete it */
USE Master
GO

DROP DATABASE LearnSQL


What actually sets SQL Server apart from other programming languages is the way SQL Server processes its code. Generally, most programming languages process statement from top to bottom. By contrast, SQL Server processes them in a unique order which is known as Logical Query Processing Phase. These phases generate a series of virtual tables with each virtual table feeding into the next phase (virtual tables not viewable). These phases and their orders are given as follows:

1. FROM
2. ON
3. OUTER
4. WHERE
5. GROUP BY
6. CUBE | ROLLUP
7. HAVING
8. SELECT
9. DISTINCT
10 ORDER BY
11. TOP