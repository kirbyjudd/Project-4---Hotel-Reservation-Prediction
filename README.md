### Group 5 Project 4 - Hotel Reservation Cancellation Prediction

### Introduction

The dataset source (Dataset Source: https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset) provided hotel reservation information with the intent of trying to predict whether or not a customer is going to cancel a reservation. The reservation data covers a three year time period from Portugal. The source data was modified as described below so that various models could be tested in order to determine if accurate predictions could be made with regards to cancellations.

### Preprocessing and Data Cleanup

The original dataset was reviewed during preprocessing in order to streamline the data for model development.

The following steps were performed on the data.

1. The company column contained a significant number of null values and was dropped.
2. The reservation_status_date column was a string value representing date of the reservation. The number of days or lead 
   time of the reservation was already captured in another column as an integer, therefore, this column was also dropped.
3. Many of the columns contained data in string and unstructured text format that would make analysis difficult, therefore, numerous
   tables were added as lookup/data definition tables and the values were replaced with corresponding integer id values.
4. A new column "international" was added that is a binary field indicating whether the country of residence for the individual making
   the reservation was domestic or international.
5. A new column "room_type_fulfilled" was added which compared the room type that was requested with the room type that was actually
   provided in order to determine if a change in room type was a contributing factor to cancellations.
6. The arrival_date_month column was changed from string to an integer indicator for the month (1-12).
7. The reservatoin_status column was dropped since it provided cancellation results which
   was preventing the model from effectively determining which features were contributing to
   cancellations.

### Database Creation, Imports, and Jupyter Notebook Database Connection

Once the changes to the data were complete the following instructions were provided to create, import, and validate the csv files:

Directions to setup hotel_bookings_db (From: hotel_bookings_start_here.txt)
1. Create a new database using pgAdmin named: hotel_bookings_db
2. Open a new query window. Copy and paste the entire contents of this file into
   the window. Run Execute.
3. Navigate to hotel_bookings_db>Schemas>public>Tables. Right click on Tables and
   select refresh.
4. Right click on the country table and select Import/Export Data. 
   Select Import. Set the path to the file to country_import.csv. Change format to csv.
   Click on Options in the Import/Export menu.
   Ensure Header is set to on. Scroll down to NULL Strings and to the value to: NULL
   Select Ok to import the file.
5. Repeat step 4 for the following tables/csv files:
   customer/customer_import.csv
   misc/misc_import.csv
   market/market_import.csv
   rooms/rooms_import.csv
   status/status_import.csv
   support/support_import.csv
   hotel_bookings/hotel_bookings_import.csv
6. Open a new query window and execute the following code:
   ALTER TABLE hotel_bookings
   DROP COLUMN company;
7. Open a new query window and execute the following code:
   ALTER TABLE hotel_bookings
   DROP COLUMN reservation_status_date;
8. Open a new query window and execute the following code:
   ALTER TABLE hotel_bookings
   DROP COLUMN reservation_status;
9. Perform a select statement on each table to validate imports.

Once the database was established psycopg2 was used to esablish a connection string from the Jupyter Notebook to the local Postgres database.

### Model Development

Data Stratification 

As a result of the size of the dataset the data was stratified. Testing was complete and validated that our data of interest was 61% and 39% in both the full and stratified data sets.

Three models were run against the data:

Logistic Regression = 89%

Random Forest = 85%

Decision Tree = 79%


In order to evaluate model performance on the test data the following were generated:

Confustion Matrix

Accuracy Score

Classification Report

### Conclusion and Recomendations

The models are effective in identifying features contributing to cancellations.

Three features most important to predict cancellations:
   Deposit Type

   Country of Origin (Domestic vs International)

   Lead Time of Reservation

Recommendations to Reduce Cancellations:
   Always charge a deposit

	Cater to international clients

	Reduce early booking window

	Optimize price strategies
   

### Limitations

1. Dataset from single country “Portugal”: The analysis is based on hotel reservation data from Portugal.  As a result, the findings may not be directly applicable to hotels in other countries with different travel patterns and preferences.

2. Data Age (2015-2017): The data used in the analysis spans from 2015 to 2017, which may not fully capture the current trends and dynamics in the hospitality industry. 

3. Pre-COVID Era: The dataset predates the COVID-19 pandemic, which significantly impacted the travel and hospitality industry. As a result, the predictive models may not accurately account for the post-COVID travel economy and uncertainties. 




