# Employee Performance Analysis Dashboard

## Dashboard Preview
![image](https://github.com/user-attachments/assets/5051ca4c-1001-4b07-a9e8-01c3131b3892)


## Overview
This is a comprehensive data analyst portfolio project focused on employee performance analysis and HR analytics. Using a dataset with five files, I demonstrate how to preprocess and clean the data in **Google BigQuery**. 
Afterward, the cleaned data is uploaded into **Google Looker Studio** (formerly Google Data Studio) to create an insightful dashboard.

The key steps in the process include, from **data preprocessing** to **building a professional dashboard**, including defining a **business problem statement** and utilizing **ChatGPT** to assist with certain tasks.

This project covers essential topics for data analysts, including:
- **Google BigQuery basics**
- **Google Looker Studio dashboards**
- **Portfolio project creation**

This is an ideal resource for anyone looking to build their **data analyst portfolio** or gain insights into **HR analytics**.

## Key Sections
- **Dataset Overview & Business Problem Definition**
- **Data Preprocessing in Google BigQuery**
- **Dashboard Creation in Looker Studio**
- **Key Insights & Analysis**


## Tools & Technologies Used
- **Google BigQuery** for data processing
- **Google Looker Studio** for visualization
- **ChatGPT** for assistance in project execution

## Video Walkthrough
For a step-by-step walkthrough of the project, and the dataset check out the original tutorial on YouTube: <br>
https://www.youtube.com/watch?v=sljBV59x_mM&list=PLYUd-PJHEzRAGR2Hb5w2qTs2lt_r-K-K2&index=9

## How to Use This Project
1. Download the dataset from Github <br>
    (https://github.com/WajihaAhmed99/Data-Analyst-Portfolio-Project-Google-BigQuery-Looker-Studio-Employee-Performance-Analysis/tree/main).
2. Upload the data to Google BigQuery.
3. Follow the data preprocessing steps.
4. Import cleaned data into Google Looker Studio.
5. Build a dashboard and derive insights.

## Dashboard <br>
https://lookerstudio.google.com/s/o4H99Fh1iwA

## BigQuery Query Scripts

```sql

SELECT 
    EmployeeID, 
    CONCAT(FirstName, " ", LastName) AS Employee_Name,
    Gender, 
    BusinessTravel, 
    Department, 
    `DistanceFromHome KM`, 
    Ethnicity, 
    Education, 
    EducationField, 
    JobRole, 
    MaritalStatus, 
    StockOptionLevel, 
    OverTime, 
    HireDate, 
    Attrition, 
    YearsAtCompany, 
    YearsInMostRecentRole, 
    YearsSinceLastPromotion, 
    YearsWithCurrManager,
     CASE 
        WHEN Age BETWEEN 19 AND 25 THEN '19-25'
        WHEN Age BETWEEN 26 AND 32 THEN '26-32'
        WHEN Age BETWEEN 33 AND 39 THEN '33-39'
        WHEN Age BETWEEN 40 AND 45 THEN '40-45'
        WHEN Age BETWEEN 46 AND 51 THEN '46-51'
        ELSE 'Unknown'
    END AS Age_Group,
    CASE 
        WHEN State = 'CA' THEN 'California'
        WHEN State = 'IL' THEN 'Illinois'
        WHEN State = 'NY' THEN 'New York'
        ELSE 'Unknown'
    END AS Full_State_Name,
    CASE 
        WHEN Salary BETWEEN 20387 AND 100000 THEN '20K-100K'
        WHEN Salary BETWEEN 100001 AND 200000 THEN '100K-200K'
        WHEN Salary BETWEEN 200001 AND 300000 THEN '200K-300K'
        WHEN Salary BETWEEN 300001 AND 400000 THEN '300K-400K'
        WHEN Salary BETWEEN 400001 AND 500000 THEN '400K-500K'
        WHEN Salary BETWEEN 500001 AND 547204 THEN '500K-550K'
        ELSE 'Unknown'
    END AS Salary_Bin,
FROM `golden-torch-451215-m8.HR.Employee dataset`;

--Join employee and education level--

CREATE TABLE `golden-torch-451215-m8.HR.Table1` AS
SELECT 
    EmployeeID, 
    CONCAT(FirstName, " ", LastName) AS Employee_Name,
    Gender, 
    BusinessTravel, 
    Department, 
    `DistanceFromHome KM`, 
    Ethnicity, 
    EducationField, 
    JobRole, 
    MaritalStatus, 
    StockOptionLevel, 
    OverTime, 
    HireDate, 
    Attrition, 
    YearsAtCompany, 
    YearsInMostRecentRole, 
    YearsSinceLastPromotion, 
    YearsWithCurrManager,
     CASE 
        WHEN Age BETWEEN 19 AND 25 THEN '19-25'
        WHEN Age BETWEEN 26 AND 32 THEN '26-32'
        WHEN Age BETWEEN 33 AND 39 THEN '33-39'
        WHEN Age BETWEEN 40 AND 45 THEN '40-45'
        WHEN Age BETWEEN 46 AND 51 THEN '46-51'
        ELSE 'Unknown'
    END AS Age_Group,
    CASE 
        WHEN State = 'CA' THEN 'California'
        WHEN State = 'IL' THEN 'Illinois'
        WHEN State = 'NY' THEN 'New York'
        ELSE 'Unknown'
    END AS Full_State_Name,
    CASE 
        WHEN Salary BETWEEN 20387 AND 100000 THEN '20K-100K'
        WHEN Salary BETWEEN 100001 AND 200000 THEN '100K-200K'
        WHEN Salary BETWEEN 200001 AND 300000 THEN '200K-300K'
        WHEN Salary BETWEEN 300001 AND 400000 THEN '300K-400K'
        WHEN Salary BETWEEN 400001 AND 500000 THEN '400K-500K'
        WHEN Salary BETWEEN 500001 AND 547204 THEN '500K-550K'
        ELSE 'Unknown'
    END AS Salary_Bin,
    E1.EducationLevel
FROM `golden-torch-451215-m8.HR.Employee dataset` E
JOIN `golden-torch-451215-m8.HR.education level` E1
ON E.Education = E1.EducationLevelID;

--Create Table 2--
CREATE TABLE `golden-torch-451215-m8.HR.Table2` AS
SELECT EmployeeID, 
PerformanceID, 
ReviewDate, 
E5. SatisfactionLevel AS EnvironmentSatisfaction, 
E6. SatisfactionLevel AS JobSatisfaction, 
E7. SatisfactionLevel AS RelationshipSatisfaction, 
TrainingOpportunitiesWithinYear, 
TrainingOpportunitiesTaken, 
WorkLifeBalance, 
E3. RatingLevel AS SelfRating, 
E4. RatingLevel AS ManagerRating 
FROM `golden-torch-451215-m8.HR.Performance rating` E2
JOIN `golden-torch-451215-m8.HR.Rating Level` E3
ON E2.SelfRating = E3.RatingID
JOIN `golden-torch-451215-m8.HR.Rating Level` E4
ON E2.SelfRating = E4.RatingID
JOIN `golden-torch-451215-m8.HR.Satisfied Level` E5
ON E2.EnvironmentSatisfaction = E5.SatisfactionID
JOIN `golden-torch-451215-m8.HR.Satisfied Level` E6
ON E2.JobSatisfaction = E6.SatisfactionID
JOIN `golden-torch-451215-m8.HR.Satisfied Level` E7
ON E2.RelationshipSatisfaction = E7.SatisfactionID;


-- Identifying and deleting duplicate and null values --
-- Identifying null values in table 1
SELECT *
FROM `golden-torch-451215-m8.HR.Table1`
WHERE EmployeeID IS NULL
OR Employee_Name IS NULL
OR Gender IS NULL 
OR BusinessTravel IS NULL
OR Department IS NULL
OR `DistanceFromHome KM` IS NULL
OR Ethnicity IS NULL
OR EducationField IS NULL
OR JobRole IS NULL
OR MaritalStatus IS NULL
OR StockOptionLevel IS NULL
OR OverTime IS NULL
OR HireDate IS NULL
OR Attrition IS NULL
OR YearsAtCompany IS NULL
OR YearsInMostRecentRole IS NULL
OR YearsSinceLastPromotion IS NULL
OR YearsWithCurrManager IS NULL
OR Age_Group IS NULL
OR Age_Group IS NULL
OR Full_State_Name IS NULL
OR Salary_Bin IS NULL
OR Salary_Bin IS NULL
OR EducationLevel IS NULL;

-- Identifying duplicate values in table 1
SELECT EmployeeID,
COUNT(*) AS Total
FROM `golden-torch-451215-m8.HR.Table1`
GROUP BY EmployeeID
Having Count(*) >1;


-- Identifying null values in table 2 
SELECT *
FROM `golden-torch-451215-m8.HR.Table2`
WHERE EmployeeID IS NULL
OR PerformanceID IS NULL
OR ReviewDate IS NULL
OR EnvironmentSatisfaction IS NULL
OR JobSatisfaction IS NULL
OR RelationshipSatisfaction IS NULL
OR TrainingOpportunitiesWithinYear IS NULL
OR TrainingOpportunitiesTaken IS NULL
OR WorkLifeBalance IS NULL
OR SelfRating IS NULL
OR ManagerRating IS NULL;
-- Identifying duplicate values in table 2 --
SELECT PerformanceID,
COUNT(*) AS Total
FROM `golden-torch-451215-m8.HR.Table2`
GROUP BY PerformanceID
Having Count(*) >1;

```

## Contact & Portfolio
If you have any questions or feedback, feel free to reach out!

