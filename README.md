# SQL Queries and Procedures Usage Guide
### Database and Table Creation

## Create Database
- **Description:** This step initializes a new database called GlobalCarDetails. This is the first step in setting up a structured environment for storing car-related data.


## Create Manufacturers Table

- **Description:** This table stores information about car manufacturers, including a unique ID, the manufacturer's name, and the country of origin. This table serves as a reference for car manufacturers.


## Create Models Table

- **Description:** This table keeps track of car models with a unique ID and model name. It is used to catalog the different car models available.
  
## Create Cars Table

- **Description:** This table records details about specific cars, including a unique ID, associated manufacturer and model IDs, the production year, and the price of the car. It links to the Manufacturers and Models tables to provide a complete record of each car's origin and specifications.
  
## Data Insertion

## Insert Manufacturers
- **Description:** Adds new records to the MANUFACTURERS table, specifying the manufacturer’s name and country.

## Insert Models

- **Description:** Adds new records to the Models table, specifying the model name.

## Insert Cars

- **Description:** Inserts new records into the Cars table with information about the manufacturer, model, year of manufacture, and price. This step is essential for populating the database with actual car data.

**Data Retrieval**

## Select All Cars

- **Description:** Retrieves and displays all records from the Cars table, including details of the manufacturer, model, year, and price.
 
## Select Cars by Manufacturer

- **Description:** Fetches all cars associated with a specific manufacturer. Useful for viewing all models produced by a particular manufacturer.
  
## Select Cars by Model

**Description:** Retrieves cars based on a specific model. This helps in finding all cars of a given model.

## Data Updating
## Update Car Price

- **Description:** Modifies the price of a car in the Cars table based on the car’s ID. This is used for adjusting prices as needed.

## Update Car Year

- **Description:** Updates the production year of a car. This helps in correcting or updating information about the car’s manufacturing year.

## Data Deletion
## Delete Car

- **Description:** Removes a specific car record from the Cars table based on the car’s ID. This is used for deleting obsolete or incorrect entries.
  
## Delete Model

- **Description:** Deletes a car model from the Models table. This might be used if a model is discontinued or needs to be removed for other reasons.
  
## Delete Manufacturer

- **Description:** Removes a manufacturer record from the MANUFACTURERS table. This might be necessary if a manufacturer is no longer relevant or was added by mistake.


## Stored Procedures
## Add Manufacturer

- **Description:** A stored procedure to add a new manufacturer with the provided name and country.

## Add Model

- **Description:** A stored procedure to add a new car model with the provided model name.
  
## Add Car

- **Description:** A stored procedure to add a new car with details including manufacturer ID, model ID, year, and price.
  
## Update Car Details

- **Description:** A stored procedure to update details of an existing car, such as its price or production year.
  
## Remove Car

- **Description:** A stored procedure to delete a car record by its ID.

# -- Step 1: Create the database
CREATE DATABASE IF NOT EXISTS GlobalCarDetails;

-- Step 2: Use the database
USE GlobalCarDetails;

-- Step 3: Create the Manufacturers table
CREATE TABLE IF NOT EXISTS Manufacturers (
    ManufacturerID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Country VARCHAR(100) NOT NULL
);

-- Step 4: Create the Models table
CREATE TABLE IF NOT EXISTS Models (
    ModelID INT AUTO_INCREMENT PRIMARY KEY,
    ModelName VARCHAR(100) NOT NULL
);

-- Step 5: Create the Cars table
CREATE TABLE IF NOT EXISTS Cars (
    CarID INT AUTO_INCREMENT PRIMARY KEY,
    ManufacturerID INT,
    ModelID INT,
    Year INT,
    Price DECIMAL(15, 2),
    FOREIGN KEY (ManufacturerID) REFERENCES Manufacturers(ManufacturerID),
    FOREIGN KEY (ModelID) REFERENCES Models(ModelID)
);

-- Step 6: Create the Countries table
CREATE TABLE IF NOT EXISTS Countries (
    CountryID INT AUTO_INCREMENT PRIMARY KEY,
    CountryName VARCHAR(100) NOT NULL
);

-- Step 7: Create the Car_Sales table
CREATE TABLE IF NOT EXISTS Car_Sales (
    SaleID INT AUTO_INCREMENT PRIMARY KEY,
    CarID INT,
    SaleDate DATE,
    SalePrice DECIMAL(15, 2),
    CountryID INT,
    FOREIGN KEY (CarID) REFERENCES Cars(CarID),
    FOREIGN KEY (CountryID) REFERENCES Countries(CountryID)
);

-- Step 8: Insert data into Manufacturers table
INSERT INTO Manufacturers (Name, Country)
VALUES 
('Audi', 'Germany'),
('BMW', 'Germany'),
('Toyota', 'Japan'),
('Ford', 'USA'),
('Hyundai', 'South Korea'),
('Fiat', 'Italy');

-- Step 9: Insert data into Models table
INSERT INTO Models (ModelName)
VALUES 
('Q5'),
('X5'),
('Corolla'),
('Mustang'),
('Verna'),
('CR-V');

-- Step 10: Insert data into Cars table
INSERT INTO Cars (ManufacturerID, ModelID, Year, Price)
VALUES 
(1, 1, 1990, 2500000),
(2, 2, 1987, 3500000),
(3, 3, 1965, 5000000),
(4, 4, 1999, 2200000),
(5, 5, 2000, 3500000),
(6, 6, 1980, 5500000);

-- Step 11: Insert data into Countries table
INSERT INTO Countries (CountryName)
VALUES 
('Germany'),
('Japan'),
('USA'),
('South Korea'),
('Italy');

-- Step 12: Insert data into Car_Sales table
INSERT INTO Car_Sales (CarID, SaleDate, SalePrice, CountryID)
VALUES 
(1, '2024-01-15', 1900000, 1),
(2, '2024-02-20', 2900000, 1),
(3, '2024-03-10', 430000, 2),
(4, '2024-01-25', 1700000, 3),
(5, '2024-02-15', 4300000, 4);






-- Query1: Display all records from the Manufacturers table
SELECT * FROM Manufacturers;

-- Query2: Show only the Name and Country of all manufacturers
SELECT Name, Country FROM Manufacturers;

-- Query3: Retrieve the ModelID and ModelName from the Models table
SELECT ModelID, ModelName FROM Models;

-- Query4: Display all cars manufactured after the year 2000
SELECT * FROM Cars WHERE Year > 2000;

-- Query5: Find all cars with a price greater than 3,000,000
SELECT * FROM Cars WHERE Price > 3000000;

-- Query6: Count the number of manufacturers
SELECT COUNT(*) FROM Manufacturers;

-- Query7: Find the maximum price of all cars
SELECT MAX(Price) FROM Cars;

-- Query8: Retrieve the minimum price from the Car_Sales table
SELECT MIN(SalePrice) FROM Car_Sales;

-- Query9: Display distinct countries from the Countries table
SELECT DISTINCT CountryName FROM Countries;

-- Query10: Find all car models that start with the letter 'C'
SELECT * FROM Models WHERE ModelName LIKE 'C%';

-- Query11: Retrieve all cars sold in 2024
SELECT * FROM Car_Sales WHERE YEAR(SaleDate) = 2024;

-- Query12: Count the number of car models by each manufacturer
SELECT ManufacturerID, COUNT(*) AS ModelCount FROM Cars GROUP BY ManufacturerID;

-- Query13: Find the total sales price of all cars sold
SELECT SUM(SalePrice) FROM Car_Sales;

-- Query14: Display all records from the Countries table where the country name is not 'Germany'
SELECT * FROM Countries WHERE CountryName != 'Germany';

-- Query15: Retrieve the first 3 manufacturers from the Manufacturers table
SELECT * FROM Manufacturers LIMIT 3;

-- Query16: Display all manufacturers in alphabetical order by their name
SELECT * FROM Manufacturers ORDER BY Name ASC;

-- Query17: Find the average price of cars
SELECT AVG(Price) AS AvgPrice FROM Cars;

-- Query18: Retrieve car models that have the letter 'a' in their name
SELECT * FROM Models WHERE ModelName LIKE '%a%';

-- Query19: Count the number of cars for each model
SELECT ModelID, COUNT(*) AS CarCount FROM Cars GROUP BY ModelID;

-- Query20: Find the maximum year of manufacture for each manufacturer
SELECT ManufacturerID, MAX(Year) AS LatestYear FROM Cars GROUP BY ManufacturerID;

-- Query21: Display cars with a price between 2,000,000 and 5,000,000
SELECT * FROM Cars WHERE Price BETWEEN 2000000 AND 5000000;

-- Query22: Show cars that have either a ModelID of 1 or 4
SELECT * FROM Cars WHERE ModelID IN (1, 4);

-- Query23: Find all sales that occurred in January 2024
SELECT * FROM Car_Sales WHERE MONTH(SaleDate) = 1 AND YEAR(SaleDate) = 2024;

-- Query24: Retrieve the details of cars with a CarID of 1 or 2
SELECT * FROM Cars WHERE CarID IN (1, 2);

-- Query25: Display all manufacturers and order them by Country in descending order
SELECT * FROM Manufacturers ORDER BY Country DESC;

-- Query26: Join the Cars table with the Manufacturers table to show car details along with the manufacturer name
SELECT Cars.CarID, Cars.ManufacturerID, Cars.ModelID, Cars.Year, Cars.Price, Manufacturers.Name AS ManufacturerName
FROM Cars
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID;

-- Query27: Find the total number of cars manufactured by each manufacturer
SELECT ManufacturerID, COUNT(CarID) AS TotalCars FROM Cars GROUP BY ManufacturerID;

-- Query28: Calculate the total sales for each car model
SELECT Cars.ModelID, SUM(Car_Sales.SalePrice) AS TotalSales
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
GROUP BY Cars.ModelID;

-- Query29: Retrieve the most recent sale date for each car
SELECT CarID, MAX(SaleDate) AS LatestSaleDate FROM Car_Sales GROUP BY CarID;

-- Query30: List all cars that have not been sold
SELECT * FROM Cars WHERE CarID NOT IN (SELECT CarID FROM Car_Sales);

-- Query31: Find the average sale price for each country
SELECT Countries.CountryName, AVG(Car_Sales.SalePrice) AS AvgSalePrice
FROM Car_Sales
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
GROUP BY Countries.CountryName;

-- Query32: Count the number of sales for each car
SELECT CarID, COUNT(SaleID) AS NumberOfSales FROM Car_Sales GROUP BY CarID;

-- Query33: Find the most expensive car sold in each country
SELECT CountryID, MAX(SalePrice) AS MaxSalePrice FROM Car_Sales GROUP BY CountryID;

-- Query34: Join the Car_Sales table with Countries to show sales details along with the country name
SELECT Car_Sales.SaleID, Car_Sales.CarID, Car_Sales.SaleDate, Car_Sales.SalePrice, Car_Sales.CountryID, Countries.CountryName
FROM Car_Sales
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID;

-- Query35: Retrieve all car models along with their manufacturer's name
SELECT Models.ModelName, Manufacturers.Name AS ManufacturerName
FROM Models
INNER JOIN Cars ON Models.ModelID = Cars.ModelID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID;

-- Query36: Display all car sales where the sale price is higher than the car's original price
SELECT Car_Sales.SaleID, Car_Sales.SalePrice, Cars.Price
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
WHERE Car_Sales.SalePrice > Cars.Price;

-- Query37: Find the manufacturer with the most car models
SELECT ManufacturerID, COUNT(ModelID) AS ModelsCount
FROM Cars
GROUP BY ManufacturerID
ORDER BY ModelsCount DESC
LIMIT 1;

-- Query38: List the car models that have been sold more than once
SELECT Cars.ModelID, COUNT(Car_Sales.SaleID) AS SalesCount
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
GROUP BY Cars.ModelID
HAVING SalesCount > 1;

-- Query39: Find the average sale price for each car model
SELECT Cars.ModelID, AVG(Car_Sales.SalePrice) AS AvgSalePrice
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
GROUP BY Cars.ModelID;

-- Query40: Retrieve the car details for the most recent sale date
SELECT Cars.*, Car_Sales.SaleDate
FROM Cars
INNER JOIN Car_Sales ON Cars.CarID = Car_Sales.CarID
WHERE Car_Sales.SaleDate = (SELECT MAX(SaleDate) FROM Car_Sales);


-- Query41: Find the total number of cars sold in each country
SELECT Countries.CountryName, COUNT(Car_Sales.SaleID) AS TotalSales
FROM Car_Sales
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
GROUP BY Countries.CountryName;

-- Query42: Retrieve the car models that have the highest average sale price
SELECT Models.ModelName, AVG(Car_Sales.SalePrice) AS AvgSalePrice
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Models ON Cars.ModelID = Models.ModelID
GROUP BY Models.ModelName
ORDER BY AvgSalePrice DESC
LIMIT 1;

-- Query43: List all manufacturers along with the number of cars they have in the database
SELECT Manufacturers.Name AS ManufacturerName, COUNT(Cars.CarID) AS CarCount
FROM Manufacturers
LEFT JOIN Cars ON Manufacturers.ManufacturerID = Cars.ManufacturerID
GROUP BY Manufacturers.Name;

-- Query44: Find the most recent sale date for each manufacturer
SELECT Manufacturers.Name AS ManufacturerName, MAX(Car_Sales.SaleDate) AS LatestSaleDate
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
GROUP BY Manufacturers.Name;

-- Query45: Retrieve the average price of cars for each manufacturer
SELECT Manufacturers.Name AS ManufacturerName, AVG(Cars.Price) AS AvgCarPrice
FROM Cars
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
GROUP BY Manufacturers.Name;

-- Query46: List the top 3 most expensive cars ever sold
SELECT Car_Sales.CarID, Cars.Price, Car_Sales.SalePrice
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
ORDER BY Car_Sales.SalePrice DESC
LIMIT 3;

-- Query47: Find all manufacturers that have cars sold in more than 3 different countries
SELECT Manufacturers.Name AS ManufacturerName, COUNT(DISTINCT Car_Sales.CountryID) AS CountryCount
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
GROUP BY Manufacturers.Name
HAVING CountryCount > 3;

-- Query48: Retrieve the total sales amount for each car model, sorted by total sales in descending order
SELECT Models.ModelName, SUM(Car_Sales.SalePrice) AS TotalSales
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Models ON Cars.ModelID = Models.ModelID
GROUP BY Models.ModelName
ORDER BY TotalSales DESC;

-- Query49: Show the car models that have never been sold
SELECT Models.ModelName
FROM Models
LEFT JOIN Cars ON Models.ModelID = Cars.ModelID
LEFT JOIN Car_Sales ON Cars.CarID = Car_Sales.CarID
WHERE Car_Sales.SaleID IS NULL;

-- Query50: Find the average number of sales per car model
SELECT AVG(SalesCount) AS AvgSalesPerModel
FROM (SELECT Cars.ModelID, COUNT(Car_Sales.SaleID) AS SalesCount
      FROM Car_Sales
      INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
      GROUP BY Cars.ModelID) AS ModelSalesCounts;

-- Query51: Retrieve the manufacturer with the lowest average car price
SELECT Manufacturers.Name AS ManufacturerName, AVG(Cars.Price) AS AvgCarPrice
FROM Cars
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
GROUP BY Manufacturers.Name
ORDER BY AvgCarPrice ASC
LIMIT 1;

-- Query52: List all sales details along with the manufacturer's name and country
SELECT Car_Sales.SaleID, Car_Sales.SaleDate, Car_Sales.SalePrice, Manufacturers.Name AS ManufacturerName, Countries.CountryName
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID;

-- Query53: Find the total number of unique car models sold in each country
SELECT Countries.CountryName, COUNT(DISTINCT Cars.ModelID) AS UniqueModelsSold
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
GROUP BY Countries.CountryName;

-- Query54: Retrieve the car model with the highest number of sales
SELECT Models.ModelName, COUNT(Car_Sales.SaleID) AS SalesCount
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Models ON Cars.ModelID = Models.ModelID
GROUP BY Models.ModelName
ORDER BY SalesCount DESC
LIMIT 1;

-- Query55: Find the number of cars sold in each year, and list them in descending order
SELECT YEAR(SaleDate) AS SaleYear, COUNT(SaleID) AS NumberOfSales
FROM Car_Sales
GROUP BY YEAR(SaleDate)
ORDER BY NumberOfSales DESC;

-- Query56: Display the total sales revenue for each manufacturer
SELECT Manufacturers.Name AS ManufacturerName, SUM(Car_Sales.SalePrice) AS TotalSalesRevenue
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
GROUP BY Manufacturers.Name;

-- Query57: Find the car model with the highest average sale price in each country
SELECT Countries.CountryName, Models.ModelName, AVG(Car_Sales.SalePrice) AS AvgSalePrice
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Models ON Cars.ModelID = Models.ModelID
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
GROUP BY Countries.CountryName, Models.ModelName
HAVING AvgSalePrice = (SELECT MAX(AvgSalePrice)
                       FROM (SELECT Countries.CountryName, Models.ModelName, AVG(Car_Sales.SalePrice) AS AvgSalePrice
                             FROM Car_Sales
                             INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
                             INNER JOIN Models ON Cars.ModelID = Models.ModelID
                             INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
                             GROUP BY Countries.CountryName, Models.ModelName) AS ModelPrices
                       WHERE ModelPrices.CountryName = Countries.CountryName);

-- Query58: List the countries that have sold cars with an average sale price above 2,000,000
SELECT Countries.CountryName
FROM Car_Sales
INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
GROUP BY Countries.CountryName
HAVING AVG(Car_Sales.SalePrice) > 2000000;

-- Query59: Retrieve the list of manufacturers with cars sold in every country
SELECT Manufacturers.Name AS ManufacturerName
FROM Manufacturers
WHERE NOT EXISTS (SELECT * 
                  FROM Countries
                  WHERE NOT EXISTS (SELECT *
                                    FROM Car_Sales
                                    INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
                                    WHERE Cars.ManufacturerID = Manufacturers.ManufacturerID
                                      AND Car_Sales.CountryID = Countries.CountryID));

-- Query60: Find the median sale price of cars
SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY SalePrice) AS MedianSalePrice
FROM Car_Sales;


-- Creating a temporary table for sales data by manufacturer in 2024
CREATE TEMPORARY TABLE Temp_Sales_By_Manufacturer_2024 AS
SELECT Manufacturers.Name AS ManufacturerName, COUNT(Car_Sales.CarID) AS CarsSold
FROM Car_Sales
INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
INNER JOIN Manufacturers ON Cars.ManufacturerID = Manufacturers.ManufacturerID
WHERE YEAR(Car_Sales.SaleDate) = 2024
GROUP BY Manufacturers.Name;

-- Example usage of the temporary table
SELECT * FROM Temp_Sales_By_Manufacturer_2024;

-- Dropping the temporary table
DROP TEMPORARY TABLE IF EXISTS Temp_Sales_By_Manufacturer_2024;

-- Creating a stored procedure to retrieve car sales by year
DELIMITER //

CREATE PROCEDURE GetCarSalesByYear(IN salesYear INT)
BEGIN
    SELECT Car_Sales.SaleID, Car_Sales.CarID, Car_Sales.SaleDate, Car_Sales.SalePrice, Countries.CountryName
    FROM Car_Sales
    INNER JOIN Cars ON Car_Sales.CarID = Cars.CarID
    INNER JOIN Countries ON Car_Sales.CountryID = Countries.CountryID
    WHERE YEAR(Car_Sales.SaleDate) = salesYear;
END //

DELIMITER ;

-- Executing the stored procedure
CALL GetCarSalesByYear(2024);

-- Creating a stored procedure to get total cars sold by year
DELIMITER //

CREATE PROCEDURE GetTotalCarsSoldByYear(IN salesYear INT, OUT totalCarsSold INT)
BEGIN
    SELECT COUNT(*) INTO totalCarsSold
    FROM Car_Sales
    WHERE YEAR(SaleDate) = salesYear;
END //

DELIMITER ;

-- Declaring a variable to store the output and calling the stored procedure
SET @totalCarsSold = 0;
CALL GetTotalCarsSoldByYear(2024, @totalCarsSold);
SELECT @totalCarsSold;

-- Creating a stored procedure to insert a new car sale
DELIMITER //

CREATE PROCEDURE InsertCarSale(
    IN carID INT,
    IN saleDate DATE,
    IN salePrice DECIMAL(15,2),
    IN countryID INT
)
BEGIN
    INSERT INTO Car_Sales (CarID, SaleDate, SalePrice, CountryID)
    VALUES (carID, saleDate, salePrice, countryID);
END //

DELIMITER ;

-- Executing the insert procedure
CALL InsertCarSale(1, '2024-08-30', 2500000, 12);

-- Creating a stored procedure with conditional logic to update car prices
DELIMITER //

CREATE PROCEDURE UpdateCarPrices(IN minYear INT, IN priceIncrease DECIMAL(15,2))
BEGIN
    UPDATE Cars
    SET Price = Price + priceIncrease
    WHERE Year >= minYear;
END //

DELIMITER ;

-- Executing the update procedure to increase prices for cars manufactured in or after 2015 by $500,000
CALL UpdateCarPrices(2015, 500000);
