# Newark Airport Airline Performance

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
#### In order to understand the data, I first reviewed the source data profile Excel file which contains a description and type for each column in order to gain an understanding of which columns I would need to import.  I then explored the data by reading it into a DataFrame object and reviewing which columns had missing values and what data types were contained. Here are my findings during this exercise.
- Some fields do not import as the desired data type (i.e. "FL_DATE" is a string).
- The following fields have missing data: "Tail_Num", "Dep_Time", "Dep_Delay", "Arr_Time", "Arr_Delay".
- The rows with missing data all correspond to cancelled flights, but not all cancelled flights have missing data.
- The airline lookup table contains one missing value for "Code" which is required.  In this case, Python interpreted the code "NA" to mean NULL while importing the data.

### 3. Preparing the Data
#### 3.1 Importing the Data
In order to ensure the data types were consistent, I specified string or integer types for categorical variables and float for numeric variables.  I also specified a row-level filter to only read rows with an Origin or Destination of EWR.  


### 4. Creating the Model

### 5. Evaluating the Model

### 6. Deploying the Model

## Conclusions
