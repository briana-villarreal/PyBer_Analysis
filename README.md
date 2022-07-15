# PyBer Analysis
## Overview
### Purpose
PyBer is a ride-sharing app company, and its CEO aims to determine affordability for underserved neighborhoods and improve overall access to services. The CEO desires to obtain data regarding the total number of rides, the total number of drivers, the total fares, the average fare per ride, the average fare per driver, and the total fares for each week for the following city types: urban, suburban, and rural. These results will allow decision makers at PyBer to address any disparities in ride-sharing participation among different cities. 
## Results
### Analyzing the Data
Before analyzing the data, I added the Matplotlib inline command and imported matplotlib and pandas as dependencies. To read and store the file into a Pandas DataFrame in Jupyter Notebook, I initialized the following: "city_data_df = pd.read_csv(city_data_to_load)" and "ride_data_df=pd.read_csv(ride_data_to_load)". To increase efficiency, I merged the data into a single dataset using the pd.merge() operator on "city". 
![read csv](https://user-images.githubusercontent.com/106560739/179006948-1a1ed4da-70b8-4cbf-b2a6-acd17eb87a56.png)
![merge](https://user-images.githubusercontent.com/106560739/179006975-2fbbd565-fd88-40fc-ace3-63ace83228fb.png)
To assess the differences in ride-sharing data among the different city types, I first created three separate city type DataFrames. Each DataFrame was generated by filtering the pyber_data_df where the city type was set to “Urban”, “Suburban”, or “Rural”. Doing this allowed me to acquire the total number of rides for each city type more efficiently. To get the total number of rides, I initialized a "total_rides_by_type" variable and utilized a groupby() function to create a series of data that had the "type" of the city as the index. I then applied the count() method to the ”ride_id” column. 
![total rides](https://user-images.githubusercontent.com/106560739/179007116-d5fa0b7f-7126-40c0-9dfd-85d6c7c3ae6c.png)
Upon calculating the total rides by city type, I found that urban cities had the highest amount of rides at 1,625 and rural had the least at 125. 
I then employed the DataFrames I created for each city type to calculate the total number of drivers for urban, suburban, and rural areas. To get the total, I initialized a "total_drivers_by_type" variable and utilized the groupby() function to create a series of data that had the "type" of city as the index. I then chained the sum() method and applied it to the “driver_count” column.
![total drivers](https://user-images.githubusercontent.com/106560739/179007168-9ad05477-4df4-4bf4-aab1-2f1ca6d29ed4.png)
Upon calculating the total drivers by city type, I found that suburban had the second highest amount at 490. 
I then used the DataFrames I created for each city type to calculate the sum of the fare values for urban, suburban, and rural areas. To get the total fare amount by city type, I initialized a "total_fare_by_type" variable and utilized the groupby() function to create a series of data that had the "type" of city as the index. I then chained the sum() method and applied it to the “fare” column. 
![total fare](https://user-images.githubusercontent.com/106560739/179007237-16acafd4-2ec3-4398-b465-0c01ff100f4b.png)
Upon calculating the total fare by type of city, I found that urban areas had a high total fare of $39,854.
To calculate the average fare per ride for each city type, I initialized an "avg_fare_per_ride" variable. I then divided the "total_fare_by_type" by the "total_rides_by_type". 
![avg fare per ride](https://user-images.githubusercontent.com/106560739/179007440-dce3c92c-fbe5-4159-9e12-45c04c10cb57.png)
Upon calculating the average fare per ride for each city type, I found that rural areas had an average fare of $34.62. This number is signicantly higher than in urban and suburban areas. 
To obtain the average fare per driver for each city type, I initialized an "avg_fare_per_driver" variable. I then divided the "total_fare_by_type" by the "total_drivers_by_type".
![avg fare per driver](https://user-images.githubusercontent.com/106560739/179007475-79390e72-a465-408a-a1ee-f7f91150c87d.png)
Upon calculating the average fare per driver, I found that urban areas have the lowest amount at $16.57. 
I then created a pyber_ride_summary_df using the pd.DataFrame() operator and inserted a list of dictionaries where the keys represented column names and the values were the metrics I calculated. I cleaned the DataFrame by deleting the index name. I formatted the DataFrame using the map() function so that "Total Rides" had a thousands seperator; "Total Drivers" had a thousands seperator; "Total Fares" had a thousands seperator, dollar sign, and two decimal places; "Average Fare per Ride" had a dollar sign and two decimal places; and "Average Fare per Driver" had a dollar sign and two decimal places.
![create dataframe](https://user-images.githubusercontent.com/106560739/179007529-cd9cf50b-81e2-4e3f-a52b-8a0c52c1d391.png)
![clean and format dataframe](https://user-images.githubusercontent.com/106560739/179007543-13d0b797-7caf-45f2-8937-21c1e4d15cd8.png)
After creating the pyber_ride_summary_df, I found that rural areas have the least total drivers, yet have the highest average fare per ride and highest average fare per driver amounts. This differs significantly from their urban counterparts who have the highest amount of drivers, yet the lowest average fare per ride and the lowest average fare per driver.
To assess the data further, I analyzed the total fares for each week by city type. To do this I needed to create a multiple-line graph. Before doing so, I read the merged DataFrame, pyber_data_df. I then created a new DataFrame, named fare_for_date_df, with multiple indices using the groupby() function on the “type” and “data columns of the pyber_data_df. I then applied the sum() method on the “fare” column to show the total fare amount for each date. I also reset the index on the fare_for_date_df. 
![read dataframe](https://user-images.githubusercontent.com/106560739/179099258-e0c87d1c-4e3b-42d5-bad7-837071f51073.png)
![fare for date create df](https://user-images.githubusercontent.com/106560739/179099272-abdfc3b0-ff74-4f3a-8b46-cfd1c84d01e6.png)
![reset the index](https://user-images.githubusercontent.com/106560739/179099275-16a4cb90-a1ba-4078-af82-0c4e5d806e25.png)
I created a pivot table, named fare_for_date_pivot, utilizing the pivot() function to covert the fare_for_date_df so that the index is the “date”, each column is the city “type”, and the values are the “fare”. 
![fare for date pivot](https://user-images.githubusercontent.com/106560739/179099343-e36f988e-e173-4f29-8405-00b8030aea63.png)
I then created a new DataFrame, named fares_Jan_April_df, by using the loc[] method on the desired date ranges in the fare_for_date_pivot. I reset the index of the fares_Jan_April_df to a datetime data type using pd.to_datetime() function. I then checked that the datatype for the index was datetime by using the df.info() operator.
![pivot with loc](https://user-images.githubusercontent.com/106560739/179099411-27ab66ed-90e9-4b44-b3c0-cf59608935de.png)
![index to datetime](https://user-images.githubusercontent.com/106560739/179099466-77d1abd5-42a1-4b62-b3bc-3338e3795ec1.png)
![check datetime](https://user-images.githubusercontent.com/106560739/179099476-49df7def-5c56-4f2d-b52c-ec0c7274a88d.png)
I then created a new DataFrame, named sum_of_fare_df, using the resample() function. I resampled the data in weekly bins and applied the sum() method to get the total fares for each week. 
![create df with resample()](https://user-images.githubusercontent.com/106560739/179099508-ff787330-c41e-4378-80b3-0a99df72620b.png)
![df output](https://user-images.githubusercontent.com/106560739/179099513-4261f66f-ecf1-4a0d-8cd6-4756573172de.png)
Upon creating the sum_of_fare_df, I found that suburban areas had the highest total fare amount in February and the lowest total fare amount in January. Rural areas had the highest total fare amount in April and the lowest total fare amount in January. Urban areas had the highest total fare amount in March and the lowest total fare amount in January.
To display these findings, I created a graph using the object-oriented interface method and the df.plot() method. I used the Matplotlib “fivethirtyeight” graph style. I then annotated the y-axis and the title. 
![generate graph](https://user-images.githubusercontent.com/106560739/179127058-d6ffce97-6d31-4029-adf1-64b28d3a0d9c.png)
![graph](https://user-images.githubusercontent.com/106560739/179127066-99c18fb0-f540-44b1-9d6a-59c3c34a95c1.png)
Upon generating the graph, I found that urban areas had the overall highest amount for total fare by city type between January and April. Urban areas had the highest total fares in March and the lowest total fares in January. Suburban areas differed as their highest total fares were observed in February and their lowest total fares were in January. Rural areas had the overall lowest amount for total fares by city type between January and April. Rural areas had the highest total fares in April and the lowest total fares in January. 
## Summary
### Recommendations
Based on the results, I recommend three business strategies to the CEO to address disparities among the city types. First, I suggest lowering the average fare amount per ride in rural areas. Rural areas have the fewest total rides. Therefore if the average fare amount per ride were lowered, more individuals in rural areas may participate as customers to PyBer. This would then serve to increase the total number of rides and, in turn, expand revenue. Second, I recommend that the total number of drivers in rural areas be increased through incentives. If PyBer offers compensation for rural employees, the amount of drivers would increase along with the total number of rides. This would serve to benefit PyBer as it enhances employee satisfaction, aids in customer acquisition, and increases revenue. Third, I suggest that average fare per ride in urban areas be increased to an amount comprable to suburban and rural areas. This would level out the prices of rides amongst the city types and effectively increase revenue. 
cities are disproportionately affected by fare amounts. Lowering fare amount per ride may increase the total number of rides as more individuals 
