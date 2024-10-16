## MGH Project
### Table of Contents
 - [Project Overview](#project-overview)
 - [Exploratory Data Analysis](#exploratory-data-analysis)
 - [Findings](#findings)
 - [Recommendations](#recommendations)



#### Project Overview
This project delves into a thorough analysis of six datasets provided by Massachusetts General Hospital (MGH), one of the leading healthcare institutions in the U.S. The aim is to uncover meaningful insights related to healthcare trends, patient outcomes, and organizational efficiency. Our analysis revolves around five key hypotheses focusing on provider utilization, mortality rates across age groups, racial health disparities, revenue generation by encounter type, and the effectiveness of payer coverage.

#### Exploratory Data Analysis
Data Preparation.
The analysis began with extracting six tables from an initial dataset, centering on the encounter table. This foundational step ensured that our data was reliable and ready for analysis. We conducted a careful review of the data types and addressed any discrepancies to maintain integrity. Using Power Query, we optimized our resource usage, applying the "close and load" option with "connection only" settings to keep efficient access to the dataset.

Data Processing Tools.
 1. Power Query: This was our first step for data extraction and quality checks. We addressed discrepancies to build a solid foundation for our analysis.

2. Alteryx: After importing the dataset, we utilized various tools for data cleansing, such as removing null values and duplicates. We also calculated patient ages and standardized gender entries, saving the cleaned data in both CSV and YXMD formats for future use.

3. SQL: The refined datasets were then imported into SQL for deeper analysis. We executed complex queries and joined tables to integrate datasets, which helped us gain a better understanding of patient and provider interactions.

```
/*Organizations with more than the average revenue */
SELECT * 
FROM mghdata.organization
WHERE REVENUE > (SELECT round(Avg(REVENUE),2)   Avg_revenue
FROM mghdata.organization);

/*STORE PROCEDURE  */

SELECT DISTINCT pd.Id,pd.SSN,pd. BIRTH_DATE,pd.DEATH_DATE,pd.PASSPORT,pd.FULL_NAME,pd.GENDER,pd.ADDRESS,pd.CITY,pd.COUNTY,pd.ZIP,ed.ENCOUNTER_CLASS,pd.HEALTHCARE_EXPENSES,pd.HEALTHCARE_COVERAGE,ed.`START`,ed.`STOP`
FROM mghdata.patients pd
JOIN 
mghdata.encounters ed ON pd.Id = ed.PATIENT;

delimiter $$
create procedure mghdata.patients(IN FULL_NAME VARCHAR(100))
begin
SELECT DISTINCT pd.SSN,pd.FULL_NAME,pd. BIRTH_DATE,pd.DEATH_DATE,pd.GENDER,ed.`DESCRIPTION`,ed.ENCOUNTER_CLASS,ed.`START`,ed.`STOP`,
pd.ADDRESS,pd.CITY,pd.COUNTY,pd.HEALTHCARE_EXPENSES,pd.HEALTHCARE_COVERAGE
FROM mghdata.patients pd
JOIN 
mghdata.encounters ed ON pd.Id = ed.PATIENT
where pd.FULL_NAME = FULL_NAME;
end $$
delimiter ;

call mghdata.patients();
drop procedure mghdata.patients;


/*join on providers and organizations*/
SELECT dp.NAME,od.NAME,dp.GENDER,dp.SPECIALITY,dp.UTILIZATION,dp.ADDRESS,dp.CITY,dp.STATE,dp.ZIP
FROM mghdata.providers dp
JOIN
mghdata.organization od ON dp.ORGANIZATION = od.Id;

/* store procedure on providers*/
delimiter $$
create procedure mghdata.provider(IN Provider_Name VARCHAR(100))
begin
SELECT dp.NAME   PROVIDER_NAME,od.NAME   ORGANIZATION,dp.GENDER,dp.SPECIALITY,dp.UTILIZATION,dp.ADDRESS,dp.CITY,dp.STATE,dp.ZIP
FROM mghdata.providers dp
JOIN
mghdata.organization od ON dp.ORGANIZATION = od.Id
where dp.NAME = Provider_Name;
end $$
delimiter ;

call mghdata.provider();
drop procedure mghdata.provider;



SELECT mo.CITY,count(mp.SPECIALITY)   Count_of_speciality
FROM mghdata.organization mo
JOIN
mghdata.providers mp ON mo.Id = mp.ORGANIZATION
GROUP BY CITY
ORDER BY Count_of_speciality DESC;

/* Patients who spent more than one hour at the hospitals */
SELECT pa.FULL_NAME,timediff(ec.`STOP`,ec.`START`)   TIME
FROM mghdata.patients pa
JOIN
mghdata.encounters ec ON pa.Id = ec.PATIENT
WHERE timediff(ec.`STOP`,ec.`START`) > '01:00:00';

```

Methodologies.
We employed statistical analysis and data visualization techniques to test each hypothesis:

 - General Practitioners Dominance: We analyzed provider demographics and utilization patterns to assess the proportion of general practitioners in the healthcare system.
 - Age and Mortality: We examined mortality rates across different age groups, using descriptive statistics to identify trends and correlations.
 - Race and Disease Prevalence: We looked into hospital encounters and diagnoses among racial demographics to pinpoint health disparities.
 - Revenue Generation by Encounter Type: We compared revenue from various encounter types to identify which services were the most profitable.
 - Payer Coverage Analysis: We assessed the effectiveness of major insurance providers in terms of coverage across different healthcare categories.

#### Findings
1. General Practitioners: Our analysis confirmed that general practitioners represent the largest segment of healthcare providers, underscoring their critical role in the system.

2. Older Age Groups: We found that older age groups have significantly higher mortality rates, confirming the link between age and health risks.

3. Racial Health Disparities: White individuals exhibited higher prevalence rates for various illnesses, suggesting the existence of health disparities among racial groups.

4. Revenue Generation: Ambulatory encounters proved to generate more revenue than inpatient and emergency services, highlighting the financial viability of outpatient care.

5. Payer Coverage: Medicaid, BlueCross BlueShield, and Medicare showed comprehensive coverage, emphasizing their importance in facilitating patient access to healthcare.



![MGH Dashboard](https://github.com/user-attachments/assets/6b216fa4-85f0-4d63-b3f5-d33ed1e69b00)


#### Recommendations
Based on our findings, we recommend:

 - Resource Allocation: Increase support for general practitioners and expand outpatient services to enhance revenue generation.
 - Geriatric Care Strategies: Implement targeted interventions for older patients to improve health outcomes and optimize resource management.
 - Addressing Health Disparities: Develop programs aimed at reducing illness prevalence in underrepresented racial groups to promote equitable access to healthcare.
 - Insurance Provider Collaboration: Work closely with major payers to ensure coverage gaps are addressed, particularly in high-need areas.
