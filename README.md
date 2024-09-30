## Project Overview
The purpose of this analyses is to understand how common markers like blood pressure, serum cholesterol, heart rate, etc., contribute to the presence of cardiovascular diseases. I also drew some correlations between patients' age, heart rate, the presence of chest pain and heart disease.

## File Source
This file was obtained from Kaggle's open source repository. The following link leads to the cardiovascular health analysis notebook by Jocelyn Dumlao: [Click Here](https://www.kaggle.com/code/jocelyndumlao/cardiovascular-health-analysis/notebook#%EF%AE%A9%D9%A8%D9%80%E2%9D%A4%EF%B8%8F%EF%AE%A9%D9%A8%D9%80%EF%AE%A9%EF%AE%A9Exploratory-Data-Analysis-(EDA)%F0%9F%93%8A)

## Tools Used
To complete the study, the following data analytics tools were utilized:
1. Excel - For data import and cleaning
2. SQL - For more cleaning and analysis
3. Power BI - For visualization

## Methods and Questions
Before analyzing the dataset, I checked for duplicates, nulls, and missing values. To a large extent, the raw data was clean and ready for querying. After getting the summary statistics, I answered the following questions during the exploratory data analysis:
1. What age brackets are covered in the analysis?
2. How many men and women made up the total count? (0 for female, 1 for male)
3. How were chest pain types distributed among the participants? (0 for typical angina, 1 for atypical angina, 2 for non-anginal pain, 3 for asymptomatic)
4. What was the average resting blood pressure?
5. What is the correlation between chestpain and heartrate?
6. How is serum cholesterol distributed amongst patients?
7. What percentage of the patients had high fasting sugar levels?
8. What is the grouping of resting electrocardiogram among patients? (0 for, 1 for, 2 for)
9. What is the distribution of maximum heart rate by age?
10. How many patients have exercise-induced angina?
11. What is the percentage of patients with heart disease?
12. What is the average old peak among patients?
13. What are the metrics for the oldest patient?
14. What are the metrics for the patient with the lowest blood pressure?
15. How many patients have defects in all of their blood vessels?
16. How is the presence of a heart disease linked to gender and heart rate?

## Code
The following is the prelimianry code. Go to the code file for the full query.
```sql
----------------------------------------------------------Data Cleaning--------------------------------------------------------------------
----------------------------------------------------Look for duplicates--------------------------------------------------------------------
SELECT 
age,
gender,
chestpain,
restingBP,
serumcholesterol,
fastingbloodsugar,
restingelectro, 
maxheartrate,
exerciseangina,
oldpeak,
slope,
noofmajorvessels,
target
 FROM cardio
 GROUP BY age,
gender,
chestpain,
restingBP,
serumcholesterol,
fastingbloodsugar,
restingelectro, 
maxheartrate,
exerciseangina,
oldpeak,
slope,
noofmajorvessels,
target
HAVING COUNT(*) > 1;

----------------------------------Look for nulls---------------------------------------------------------------------------------------

SELECT * 
FROM cardio
WHERE age IS NULL
OR gender IS NULL
OR chestpain IS NULL
OR restingBP IS NULL
OR serumcholesterol IS NULL
OR fastingbloodsugar IS NULL
OR restingelectro IS NULL
OR maxheartrate IS NULL
OR exerciseangina IS NULL
OR oldpeak IS NULL
OR slope IS NULL
OR noofmajorvessels IS NULL
OR target IS NULL;

---------------------------------------------OR-------------------------------------------------------------------------------------------

SELECT * 
FROM cardio
WHERE COALESCE(age, gender, chestpain, restingBP, serumcholesterol, fastingbloodsugar, 
restingelectro, maxheartrate, exerciseangina, oldpeak, slope, noofmajorvessels, target) IS NULL;

--------------------------Since there are no nulls or duplicates, begin EDA----------------------------------------------------------------

--------------------------------Derive summary statistics----------------------------------------------------------------------------------

SELECT 
    AVG(restingelectro) AS mean_restingelectro,
    MAX(restingelectro) AS max_restingelectro,
    MIN(restingelectro) AS min_restingelectro,
    STDDEV(restingelectro) AS std_restingelectro,
    AVG(fastingbloodsugar) AS mean_fastingbloodsugar,
    MAX(fastingbloodsugar) AS max_fastingbloodsugar,
    MIN(fastingbloodsugar) AS min_fastingbloodsugar,
    STDDEV(fastingbloodsugar) AS std_fastingbloodsugar,
    AVG(chestpain) AS mean_chestpain,
    MAX(chestpain) AS max_chestpain,
    MIN(chestpain) AS min_chestpain,
    STDDEV(chestpain) AS std_chestpain,
    AVG(restingBP) AS mean_restingBP,
    MAX(restingBP) AS max_restingBP,
    MIN(restingBP) AS min_restingBP,
    STDDEV(restingBP) AS std_restingBP,
    AVG(serumcholesterol) AS mean_serumcholesterol,
    MAX(serumcholesterol) AS max_serumcholesterol,
    MIN(serumcholesterol) AS min_serumcholesterol,
    STDDEV(serumcholesterol) AS std_serumcholesterol,
    AVG(noofmajorvessels) AS AVG_noofmajorvessels,
    MAX(noofmajorvessels) AS MAX_noofmajorvessels,
    MIN(noofmajorvessels) AS MIN_noofmajorvessels,
    STDDEV(noofmajorvessels) AS MAX_noofmajorvessels
FROM cardio;
```
