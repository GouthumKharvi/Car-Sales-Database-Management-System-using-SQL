SQL Queries and Procedures Usage Guide
Database and Table Creation
Create Database

Description: This step initializes a new database called GlobalCarDetails. This is the first step in setting up a structured environment for storing car-related data.
Create Manufacturers Table

Description: This table stores information about car manufacturers, including a unique ID, the manufacturer's name, and the country of origin. This table serves as a reference for car manufacturers.
Create Models Table

Description: This table keeps track of car models with a unique ID and model name. It is used to catalog the different car models available.
Create Cars Table

Description: This table records details about specific cars, including a unique ID, associated manufacturer and model IDs, the production year, and the price of the car. It links to the Manufacturers and Models tables to provide a complete record of each car's origin and specifications.
Data Insertion
Insert Manufacturers

Description: Adds new records to the MANUFACTURERS table, specifying the manufacturer’s name and country.
Insert Models

Description: Adds new records to the Models table, specifying the model name.
Insert Cars

Description: Inserts new records into the Cars table with information about the manufacturer, model, year of manufacture, and price. This step is essential for populating the database with actual car data.
Data Retrieval
Select All Cars

Description: Retrieves and displays all records from the Cars table, including details of the manufacturer, model, year, and price.
Select Cars by Manufacturer

Description: Fetches all cars associated with a specific manufacturer. Useful for viewing all models produced by a particular manufacturer.
Select Cars by Model

Description: Retrieves cars based on a specific model. This helps in finding all cars of a given model.
Data Updating
Update Car Price

Description: Modifies the price of a car in the Cars table based on the car’s ID. This is used for adjusting prices as needed.
Update Car Year

Description: Updates the production year of a car. This helps in correcting or updating information about the car’s manufacturing year.
Data Deletion
Delete Car

Description: Removes a specific car record from the Cars table based on the car’s ID. This is used for deleting obsolete or incorrect entries.
Delete Model

Description: Deletes a car model from the Models table. This might be used if a model is discontinued or needs to be removed for other reasons.
Delete Manufacturer

Description: Removes a manufacturer record from the MANUFACTURERS table. This might be necessary if a manufacturer is no longer relevant or was added by mistake.
Stored Procedures
Add Manufacturer

Description: A stored procedure to add a new manufacturer with the provided name and country.
Add Model

Description: A stored procedure to add a new car model with the provided model name.
Add Car

Description: A stored procedure to add a new car with details including manufacturer ID, model ID, year, and price.
Update Car Details

Description: A stored procedure to update details of an existing car, such as its price or production year.
Remove Car

Description: A stored procedure to delete a car record by its ID.
