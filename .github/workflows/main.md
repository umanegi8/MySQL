/* In the scenario, you are a data analyst working with a used car dealership startup venture. 
The investors want you to find out which cars are most popular with customers so they can make sure to stock accordingly.  
This dataset contains historical sales data, including details such as car features and prices. 
Use the data to find the top 10 most popular cars and trims. Before analyzing we need to clean data.
If analyze dirty data, one could end up presenting the wrong list of cars to the investors. 
That may cause them to lose money on their car inventory investment.
*/

SELECT * FROM coursera.automobile_data;

-- Step 1: Inspect the fuel_type column (should contain only 2 ypes of fuel)

SELECT DISTINCT(fuel_type)
FROM coursera.automobile_data;
  
-- Step 2: Inspect the length column for numeric values and range
SELECT
  MIN(length) AS min_length,
  MAX(length) AS max_length
FROM coursera.automobile_data;
  
-- 3. Step 3: Fill in missing data (Missing values can create errors or skew your results during analysis)
SELECT  * FROM coursera.automobile_data 
WHERE  num_of_doors = "";

UPDATE coursera.automobile_data
SET num_of_doors = "four"
WHERE make = "dodge" AND fuel_type = "gas" AND body_style = "sedan";

UPDATE coursera.automobile_data
SET num_of_doors = "four"
WHERE make = "mazda" AND fuel_type = "diesel" AND body_style = "sedan";

-- Step 4: Identify potential errors
SELECT DISTINCT num_of_cylinders
FROM coursera.automobile_data;  -- There are two entries for two cylinders: rows 6 and 7. But the two in row 7 is misspelled. 

UPDATE coursera.automobile_data
SET num_of_cylinders = "two"
WHERE num_of_cylinders = "tow";

-- the compression_ratio column values should range from 7 to 23. 
SELECT
  MIN(compression_ratio) AS min_compression_ratio,
  MAX(compression_ratio) AS max_compression_ratio
FROM coursera.automobile_data;  -- max is 70 which is wrong. It should be 7.0

UPDATE coursera.automobile_data
SET compression_ratio = 7.0
WHERE compression_ratio = 70;

SELECT DISTINCT drive_wheels,
  LENGTH(drive_wheels) AS string_length
FROM coursera.automobile_data; -- 4wd string have four characters instead of the expected three (4wd has 3 characters)

UPDATE coursera.automobile_data
SET drive_wheels = TRIM(drive_wheels)
WHERE TRUE; -- remove extra spaces

