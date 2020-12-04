# Newark Airport Airline Performance

## File Description
- README.md -> This file contains a detailed description of the operations followed to complete this project.
- Airline Performance_v2.ipynb -> This file contains the Python code and descriptions used to evaluate the data and construct the classifier model.
- Airline Performance Data File.zip -> This zip file contains the 12 monthly flight data files, airline lookup table, and the source data profile file.

## System Requirements
The Jupyter Notebook requires Python 3 with the following libraries: pandas, os, matplotlib, and sklearn.

## Overview
This repository contains the necessary files for my Udacity Data Scientist Lesson 1 submission.  The objective for this project was to utilize the CRISP-DM process to understand, analyze, and model a selected dataset.  Because it is the holiday season and there is typically a lot of travel during this time of year, I wanted to analyze the performance of air travel into and out of Newark Liberty Airport.  Ultimately, I wanted to develop a binary classification model which would determine he probability of a flight being delayed/cancelled based on historical data.  The Jupyter Notebook file in this repository contains the Python code used for this analysis.  

## Description of Dataset
For this project, I downloaded airline flight data from the U.S. Dept of Transportation's Bureau of Transportation Statistics website (https://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=237).  The files I downloaded are contained in the .zip file on this repository.
  - 12 monthly data files containing all flights into or out of NJ airports for a calendar month
  - airline lookup file containing the relationship between airline code and airline name
  - source data profile containing a description of each field in the monthly data files

## CRISP-DM Process
### 1. Understanding the Business
#### In order to build a model to predict the probability of delay, I first needed to understand the factors which appeared to be affecting air travel.  Here are the questions I posed to help gain an understanding of air travel at Newark airport (EWR).
- What is the overall rate of delayed/cancelled flights departing EWR?
- What is the rate of delayed/cancelled flights departing EWR for each airline?
- Which airlines have the most flights and therefore the most influence on the overall delay rate?
- Is there monthly/weekly/daily seasonality?

### 2. Understanding the Data
#### First I reviewed the source data profile Excel file which contains a description and type for each column in order to gain an understanding of which columns I would need to import.  I then explored the data by reading it into a DataFrame object and reviewing which columns had missing values and what data types were contained, what types of values were found in each column, and what the distribution of data was. Here are my findings during this exercise.
- Some fields do not import as the desired data type (e.g. "FL_DATE" is a string).
- The following fields have missing data: "Tail_Num", "Dep_Time", "Dep_Delay", "Arr_Time", "Arr_Delay", however, the rows with missing data all correspond to cancelled flights, but not all cancelled flights have missing data.
- The airline lookup table contains one missing value for "Code" which is required.  In this case, Python interpreted the code "NA" to mean NULL while importing the data.

### 3. Preparing the Data
#### 3.1 Importing the Data
In order to ensure the data types were consistent, I specified string or integer types for categorical variables and float for numeric variables.  I also specified a row-level filter to only read rows with an Origin or Destination of EWR and accounted for the "NA" airline code in the lookup file.  Once all data files and lookup files were imported, I joined them into a single DataFrame using the Airline Code field.
#### 3.2 Cleaning the Data
In this step, I had to handle the inconsisent data for cancelled flights.  I chose to remove all depature/arrival information for all flights which were cancelled in order to make the analysis of times and delays consistent.  I also wanted to define a "delay" as having a departure delay time at least 30 minutes so I created a new column in the DataFrame called "Delayed" with a value of 0 for False and 1 for True.  I then created another column called "Del Canc" which uses 0 or 1 to indicate if the flight was either delayed OR cancelled.  Finally, I created a field called "Dep Block" which categorizes the departure time into six hour intervals in order to analyze the affect of time-of-day.
#### 3.3 Exploring the Data
In the exploration phase, I began by looking at the questions posed in the "Understanding the Business" section.  Ultimately I was interested in creating a model to determine the liklihood of a flight being delayed or cancelled so I looked at the delay/cancellation rate of the airport, each airline, month, weekday, and time of day.  I found that United Airlines by far has the most flights and therefore, the overall delay rate corresponds very closely to United's delay rate which is 23%.  Next I looked for seasonality througout the year.  It does appear that there is a higher rate of delays in the summer months (Jun-Aug) so "Month" may be a valuable feature for the model.  I found a similar weekly seasonality when looking at week day so, again, 'Day of Week' appeared to be a viable feature candidate.  Finally, I looked at time-of-day.  This showed a strong propensity for delays during the 18-24 time block so this appeared to be an excellent feature for the model.

### 4. Modeling the Data
#### 4.1 Choose the Algorithm
The objective of this activity was to develop a binary classification model which will determine the liklihood of a flight delay.  To accomplish this, I chose the SciKit Learn Gradient Boosting Classifier algorithm because it is one that I have used before with success to generate binary models.  
#### 4.2 Determine the Feature Set
Based on my finding during the "Exploring the Data" phase I chose "Carrier Name", "Month", "Day of Week", and "Time of Day Block" because they all seemed to have an affect on the delay rate.
#### 4.3 Split the Data
I split the data into a Training Set and a Test Set using 80% of the data for training.
#### 4.4 Encode Categorical Features
Because all of my features are categorical, I chose to use the ColumnTransformer class and OneHotEncoder to create dummy variables for each.  This creates a new column for each value of the input column and then assigns a value of 1 or 0.
#### 4.5 Train the Model
Using the encoded Training Set features and the Training Set results, I fit (or trained) the model.

### 5. Evaluating the Model
To evaluate the model, I ran a simple test using the "Score" method of the model object.  I tested it on both the Training Set and the Test Set.  For a first pass with only 4 features, I was pleasantly surprised that the score was about 78% for each.

### 6. Deploying the Model
For this exercise, "deploying the model" meant using it on my upcoming flight to determine the liklihood that it would be delayed.  My flight was scheduled for 11/24 at 2:30 PM on United Airlines.  Using these values, I created a new dataset, encoded the features, and used the model's "predict" and "predict_proba" methods to determine the likely outcome and the probability of that outcome.  I was very please to learn that my flight was predicted to be "On Time" with a 79% confidence.

## Conclusions
The detailed analysis and conclusions are summarized in my blog post at https://eric-kleen.medium.com/will-we-ever-get-there-7979244e9d8e.
